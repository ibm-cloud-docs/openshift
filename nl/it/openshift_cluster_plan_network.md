---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, rhoks, roks, rhos, multi az, multi-az, szr, mzr

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


# Pianificazione della configurazione di rete del tuo cluster
{: #plan_clusters}

Progetta una configurazione di rete per i tuoi cluster {{site.data.keyword.openshiftlong}} che soddisfi le esigenze dei tuoi carichi di lavoro e del tuo ambiente.
{: shortdesc}

Le tue applicazioni inserite in un contenitore sono ospitate su host di calcolo denominati nodi di lavoro. I nodi di lavoro sono gestiti dal master. La configurazione delle comunicazioni tra i nodi di lavoro e il master, altri servizi, Internet o altre reti private dipende da come configuri la tua rete dell'infrastruttura IBM Cloud.

È la prima volta che crei un cluster? Innanzitutto, prova l'[esercitazione relativa alla creazione di cluster OpenShift](/docs/openshift?topic=openshift-openshift_tutorial). Torna quindi qui quando sei pronto a pianificare i tuoi cluster pronti per la produzione.
{: tip}

Per pianificare la configurazione di rete del tuo cluster, per prima cosa [comprendi i principi di base della rete del cluster](#plan_basics). Quindi, puoi esaminare tre potenziali configurazioni di rete del cluster che sono adatte a scenari basati sull'ambiente, tra cui l'[esecuzione di carichi di lavoro dell'applicazione con connessione Internet](#internet-facing), l'[estensione di un data center in loco con accesso pubblico limitato](#limited-public) e l'[estensione di un data center in loco solo sulla rete privata](#private_clusters).

## Descrizione dei principi di base della rete del cluster
{: #plan_basics}

Quando crei il tuo cluster, devi scegliere una configurazione di rete in modo che alcuni componenti cluster possano comunicare tra loro e con reti o servizi esterni al cluster.
{: shortdesc}

* [Comunicazioni tra i nodi di lavoro](#worker-worker): tutti i nodi di lavoro devono essere in grado di comunicare tra loro sulla rete privata. Le comunicazioni devono essere autorizzate su più VLAN private per consentire ai nodi di lavoro che si trovano su VLAN e zone diverse di connettersi tra loro.
* [Comunicazioni tra nodo di lavoro e master e tra utente e master](#workeruser-master): i tuoi nodi di lavoro e gli utenti del cluster autorizzati possono comunicare in modo sicuro con il master Kubernetes sulla rete pubblica con TLS o sulla rete privata tramite endpoint del servizio privato.
* [Comunicazioni tra nodo di lavoro e altri servizi {{site.data.keyword.cloud_notm}} o reti in loco](#worker-services-onprem): consenti ai tuoi nodi di lavoro di comunicare in modo sicuro con altri servizi {{site.data.keyword.cloud_notm}}, come {{site.data.keyword.registrylong}}, e con una rete in loco.
* [Comunicazioni esterne alle applicazioni in esecuzione sui nodi di lavoro](#external-workers): consenti richieste pubbliche o private nel cluster e richieste fuori dal cluster a un endpoint pubblico.

### Comunicazioni tra i nodi di lavoro
{: #worker-worker}

Quando crei un cluster, i nodi di lavoro del cluster vengono connessi automaticamente a una VLAN privata e facoltativamente a una VLAN pubblica. Una VLAN configura un gruppo di nodi di lavoro e pod come se fossero collegati allo stesso cavo fisico e fornisce un canale per la connettività tra i nodi di lavoro.
{: shortdesc}

**Connessioni VLAN per i nodi di lavoro**</br>
Tutti i nodi di lavoro devono essere connessi a una VLAN privata in modo che ogni nodo possa inviare e ricevere informazioni da altri nodi di lavoro. Quando crei un cluster con nodi di lavoro che sono anche connessi a una VLAN pubblica, i tuoi nodi di lavoro possono comunicare automaticamente con il master Kubernetes sulla VLAN pubblica e sulla VLAN privata se abiliti l'endpoint del servizio privato. La VLAN pubblica fornisce anche la connettività di rete pubblica in modo che tu possa esporre le applicazioni nel tuo cluster a Internet. Tuttavia, se hai bisogno di proteggere le tue applicazioni dall'interfaccia pubblica, sono disponibili diverse opzioni per proteggere il cluster, come l'utilizzo delle politiche di rete Calico o l'isolamento del carico di lavoro della rete esterna sui nodi di lavoro edge.
* Cluster gratuiti: nei cluster gratuiti, i nodi di lavoro del cluster sono connessi a una VLAN pubblica e a una VLAN privata di proprietà di IBM per impostazione predefinita. Poiché IBM controlla le VLAN, le sottoreti e gli indirizzi IP, non puoi creare dei cluster multizona o aggiungere sottoreti al tuo cluster e puoi solo utilizzare i servizi NodePort per esporre la tua applicazione.</dd>
* Cluster standard: nei cluster standard, la prima volta che crei un cluster in una zona, viene automaticamente eseguito il provisioning di una VLAN pubblica e di una VLAN privata in tale zona per tuo conto nel tuo account dell'infrastruttura IBM Cloud. Se specifichi che i nodi di lavoro devono essere connessi solo a una VLAN privata, il provisioning automatico viene eseguito solo per la VLAN privata in quella zona. Per ogni cluster successivo che crei in tale zona, puoi specificare la coppia di VLAN che vuoi utilizzare. Puoi riutilizzare le stesse VLAN pubbliche e private che sono state create per te perché più cluster possono condividere VLAN.

Per ulteriori informazioni su VLAN, sottoreti e indirizzi IP, vedi [Panoramica della rete in {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-subnets#basics).

**Comunicazioni del nodo di lavoro attraverso sottoreti e VLAN**</br>
In diverse situazioni, i componenti del tuo cluster devono essere autorizzati a comunicare su più VLAN private. Ad esempio, se vuoi creare un cluster multizona, hai più VLAN per un cluster o hai più sottoreti sulla stessa VLAN, i nodi di lavoro che si trovano su sottoreti diverse nella stessa VLAN o in VLAN diverse non possono comunicare automaticamente tra loro. Devi abilitare il VRF (Virtual Routing and Forwarding) o lo spanning della VLAN per il tuo account dell'infrastruttura IBM Cloud.

* [VRF (Virtual Routing and Forwarding)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud): VRF consente a tutte le VLAN e sottoreti private nel tuo account dell'infrastruttura di comunicare tra loro. Inoltre, VRF è necessario per consentire ai tuoi nodi di lavoro e al master di comunicare sull'endpoint del servizio privato e di comunicare con le altre istanze {{site.data.keyword.cloud_notm}} che supportano gli endpoint del servizio privato. Per controllare se una VRF è già abilitata, utilizza il comando `ibmcloud account show`. Per abilitare VRF, esegui `ibmcloud account update --service-endpoint-enable true`. L'output di questo comando ti richiede di aprire un caso di supporto per abilitare il tuo account all'utilizzo di VRF e degli endpoint del servizio. VRF elimina l'opzione di spanning della VLAN per il tuo account poiché tutte le VLAN sono in grado di comunicare.</br></br>
Quando VRF è abilitato, qualsiasi sistema connesso a qualsiasi VLAN privata nello stesso account {{site.data.keyword.cloud_notm}} può comunicare con i nodi di lavoro del cluster. Puoi isolare il tuo cluster da altri sistemi sulla rete privata applicando delle [politiche di rete privata Calico](/docs/containers?topic=containers-network_policies#isolate_workers).</dd>
* [Spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning): se non puoi o non vuoi abilitare VRF, ad esempio se non hai bisogno che il master sia accessibile sulla rete privata o se utilizzi un dispositivo gateway per accedere al master sulla VLAN pubblica, abilita lo spanning della VLAN. Ad esempio, se hai un dispositivo gateway esistente e aggiungi quindi un cluster, le nuove sottoreti portatili ordinate per il cluster non vengono configurate sul dispositivo gateway ma lo spanning della VLAN abilita l'instradamento tra le sottoreti. Per abilitare lo spanning della VLAN, ti serve l'[autorizzazione dell'infrastruttura](/docs/containers?topic=containers-users#infra_access) **Rete > Gestisci il VLAN Spanning di rete** oppure puoi richiedere al proprietario dell'account di abilitarlo. Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud oc vlan-spanning-get`. Non puoi abilitare l'endpoint del servizio privato se scegli di abilitare lo spanning della VLAN invece di VRF.

</br>

### Comunicazioni tra nodo di lavoro e master e tra utente e master
{: #workeruser-master}

È necessario configurare un canale di comunicazione in modo che i nodi di lavoro possano stabilire una connessione al master Kubernetes. Puoi consentire le comunicazioni tra i tuoi nodi di lavoro e il master Kubernetes abilitando solo l'endpoint del servizio pubblico, gli endpoint del servizio pubblico e privato o solo l'endpoint del servizio privato.
{: shortdesc}

Per proteggere le comunicazioni sugli endpoint del servizio pubblico e privato, {{site.data.keyword.containerlong_notm}} configura automaticamente una connessione OpenVPN tra il master Kubernetes e il nodo di lavoro quando viene creato il cluster. I nodi di lavoro comunicano in modo sicuro con il master attraverso i certificati TLS e il master comunica con i nodi di lavoro attraverso la connessione OpenVPN.

**Solo endpoint del servizio pubblico**</br>
Se non vuoi o non puoi abilitare VRF per il tuo account, i tuoi nodi di lavoro possono connettersi automaticamente al master Kubernetes sulla VLAN pubblica attraverso l'endpoint del servizio pubblico.
* Le comunicazioni tra i nodi di lavoro e il master vengono stabilite in modo sicuro sulla rete pubblica attraverso l'endpoint del servizio pubblico.
* Il master è pubblicamente accessibile agli utenti del cluster autorizzati solo attraverso l'endpoint del servizio pubblico. Gli utenti del tuo cluster possono accedere in modo sicuro al tuo master Kubernetes su Internet per eseguire, ad esempio, i comandi `oc`.

**Endpoint del servizio pubblico e privato**</br>
Per rendere il tuo master accessibile pubblicamente o privatamente agli utenti del cluster, puoi abilitare gli endpoint del servizio pubblico e privato. VRF è richiesto nel tuo account {{site.data.keyword.cloud_notm}} e devi abilitare il tuo account per l'utilizzo degli endpoint del servizio. Per abilitare VRF e gli endpoint del servizio, esegui `ibmcloud account update --service-endpoint-enable true`.
* Se i nodi di lavoro sono connessi a VLAN pubbliche e private, le comunicazioni tra i nodi di lavoro e il master vengono stabilite sia sulla rete privata attraverso l'endpoint del servizio privato che sulla rete pubblica attraverso l'endpoint del servizio pubblico. Instradando
metà del traffico nodo di lavoro-master sull'endpoint pubblico e metà sull'endpoint privato, le tue comunicazioni master-nodo di lavoro sono protette da eventuali interruzioni della rete pubblica o privata. Se i nodi di lavoro sono connessi solo a VLAN private, le comunicazioni tra i nodi di lavoro e il master vengono stabilite sulla rete privata solo attraverso l'endpoint del servizio privato.
* Il master è pubblicamente accessibile agli utenti del cluster autorizzati attraverso l'endpoint del servizio pubblico. Il master è accessibile privatamente tramite l'endpoint del servizio privato se gli utenti del cluster autorizzati si trovano nella tua rete privata {{site.data.keyword.cloud_notm}} o sono connessi alla rete privata tramite una connessione VPN o {{site.data.keyword.cloud_notm}} Direct Link. Nota che devi [esporre l'endpoint master attraverso un programma di bilanciamento del carico privato](/docs/containers?topic=containers-clusters#access_on_prem) affinché gli utenti possano accedere al master tramite una connessione VPN o {{site.data.keyword.cloud_notm}} Direct Link.

**Solo endpoint del servizio privato**</br>
Per rendere il tuo master accessibile solo privatamente, puoi abilitare l'endpoint del servizio privato. VRF è richiesto nel tuo account {{site.data.keyword.cloud_notm}} e devi abilitare il tuo account per l'utilizzo degli endpoint del servizio. Per abilitare VRF e gli endpoint del servizio, esegui `ibmcloud account update --service-endpoint-enable true`. Nota che se si utilizza solo l'endpoint del servizio privato non viene applicato alcun addebito di larghezza di banda fatturata o misurata.
* Le comunicazioni tra i nodi di lavoro e il master vengono stabilite sulla rete privata attraverso l'endpoint del servizio privato.
* Il master è accessibile privatamente se gli utenti del cluster autorizzati si trovano nella tua rete privata {{site.data.keyword.cloud_notm}} o sono connessi alla rete privata tramite una connessione VPN o DirectLink. Nota che devi [esporre l'endpoint master attraverso un programma di bilanciamento del carico privato](/docs/containers?topic=containers-clusters#access_on_prem) affinché gli utenti possano accedere al master tramite una connessione VPN o DirectLink.

</br>

### Comunicazioni tra nodo di lavoro e altri servizi {{site.data.keyword.cloud_notm}} o reti in loco
{: #worker-services-onprem}

Consenti ai tuoi nodi di lavoro di comunicare in modo sicuro con altri servizi {{site.data.keyword.cloud_notm}}, come {{site.data.keyword.registrylong}}, e con una rete in loco.
{: shortdesc}

**Comunicazioni con altri servizi {{site.data.keyword.cloud_notm}} sulla rete privata o pubblica**</br>
I tuoi nodi di lavoro possono comunicare in modo automatico e sicuro con altri servizi {{site.data.keyword.cloud_notm}} che supportano gli endpoint del servizio privato, come {{site.data.keyword.registrylong}}, sulla tua rete privata dell'infrastruttura IBM Cloud. Se un servizio {{site.data.keyword.cloud_notm}} non supporta gli endpoint del servizio privato, è necessario che i nodi di lavoro siano connessi a una VLAN pubblica affinché possano comunicare in modo sicuro con i servizi sulla rete pubblica.

Se utilizzi le politiche Calico o un dispositivo gateway per controllare le reti pubbliche o private dei tuoi nodi di lavoro, devi consentire l'accesso agli indirizzi IP pubblici dei servizi che supportano gli endpoint del servizio pubblico e, facoltativamente, agli indirizzi IP privati dei servizi che supportano gli endpoint del servizio privato.
* [Consenti l'accesso agli indirizzi IP pubblici dei servizi nelle politiche Calico](/docs/containers?topic=containers-network_policies#isolate_workers_public)
* [Consenti l'accesso agli indirizzi IP privati dei servizi che supportano gli endpoint del servizio privato nelle politiche Calico](/docs/containers?topic=containers-network_policies#isolate_workers)
* [Consenti l'accesso agli indirizzi IP pubblici dei servizi e agli indirizzi IP privati dei servizi che supportano gli endpoint del servizio privato in un firewall di dispositivo gateway](/docs/containers?topic=containers-firewall#firewall_outbound)

**{{site.data.keyword.BluDirectLink}} per le comunicazioni sulla rete privata con le risorse nei data center in loco**</br>
Per connettere il tuo cluster con un data center in loco, ad esempio con {{site.data.keyword.icpfull_notm}}, puoi configurare [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link). Con {{site.data.keyword.cloud_notm}} Direct Link, crei una connessione diretta e privata tra i tuoi ambienti di rete remoti e {{site.data.keyword.containerlong_notm}} senza instradamento sull'Internet pubblico.

**Connessione VPN IPSec strongSwan sulla rete pubblica con le risorse nei data center in loco**
* Nodi di lavoro connessi a VLAN pubbliche e private: configura un [servizio VPN IPSec strongSwan ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.strongswan.org/about.html) direttamente nel tuo cluster. Il servizio VPN IPSec strongSwan fornisce un canale di comunicazione end-to-end protetto su Internet basato sulla suite di protocolli IPSec (Internet Protocol Security) standard del settore. Per configurare una connessione protetta tra il tuo cluster e una rete in loco, [configura e distribuisci il servizio VPN IPSec strongSwan](/docs/containers?topic=containers-vpn#vpn-setup) direttamente in un pod nel tuo cluster.
* Nodi di lavoro connessi solo a una VLAN privata: configura un endpoint VPN IPSec su un dispositivo gateway, ad esempio Virtual Router Appliance (Vyatta). Quindi, [configura il servizio VPN IPSec strongSwan](/docs/containers?topic=containers-vpn#vpn-setup) nel tuo cluster per utilizzare l'endpoint VPN sul tuo gateway. Se non vuoi utilizzare strongSwan, puoi [impostare la connettività VPN direttamente con VRA](/docs/containers?topic=containers-vpn#vyatta).

</br>

### Comunicazioni esterne alle applicazioni in esecuzione sui nodi di lavoro
{: #external-workers}

Consenti le richieste di traffico pubblico o privato dall'esterno del cluster alle tue applicazioni eseguite sui nodi di lavoro.
{: shortdesc}

**Traffico privato alle applicazioni del cluster**</br>
Quando distribuisci un'applicazione nel tuo cluster, potresti voler rendere l'applicazione accessibile solo agli utenti e ai servizi che si trovano sulla stessa rete privata del cluster. Il bilanciamento del carico privato è ideale per rendere la tua applicazione disponibile alle richieste provenienti dall'esterno del cluster, senza esporre l'applicazione al pubblico generale. Puoi anche utilizzare il bilanciamento del carico privato per testare l'accesso, l'instradamento delle richieste e altre configurazioni della tua applicazione, prima di esporla al pubblico tramite servizi di rete pubblica. Per consentire le richieste di traffico privato dall'esterno del cluster alle tue applicazioni, puoi creare servizi di rete Kubernetes privata, come NodePort, NLB e ALB Ingress privati. Puoi quindi utilizzare le politiche pre-DNAT Calico per bloccare il traffico verso le NodePort pubbliche dei servizi di rete privata. Per ulteriori informazioni, vedi [Pianificazione del bilanciamento del carico esterno privato](/docs/containers?topic=containers-cs_network_planning#private_access).

**Traffico pubblico alle applicazioni del cluster**</br>
Per rendere le tue applicazioni accessibili esternamente dall'Internet pubblico, puoi creare NodePort, NLB (network load balancer) e ALB (application load balancer) pubblici. I servizi di rete pubblica si connettono a questa interfaccia di rete pubblica fornendo alla tua applicazione un indirizzo IP pubblico e, facoltativamente, un URL pubblico. Quando un'applicazione viene esposta pubblicamente, chiunque disponga dell'indirizzo IP del servizio pubblico o dell'URL che hai configurato per la tua applicazione può inviare una richiesta a tale applicazione. Puoi quindi utilizzare le politiche pre-DNAT Calico per controllare il traffico verso i servizi di rete pubblica, come l'inserimento in whitelist del traffico proveniente solo da determinati indirizzi IP di origine o CIDR e il blocco di tutto il resto del traffico. Per ulteriori informazioni, vedi [Pianificazione del bilanciamento del carico esterno pubblico](/docs/containers?topic=containers-cs_network_planning#private_access).

Per ulteriore sicurezza, isola i carichi di lavoro di rete nei nodi di lavoro edge. I nodi di lavoro edge possono migliorare la sicurezza del tuo cluster consentendo a un minor numero di nodi di lavoro connessi alle VLAN pubbliche di essere accessibili esternamente e isolando il carico di lavoro della rete. Quando [etichetti i nodi di lavoro come nodi edge](/docs/containers?topic=containers-edge#edge_nodes), i pod NLB e ALB vengono distribuiti solo su quei nodi di lavoro specificati. Per impedire inoltre che altri carichi di lavoro vengano eseguiti sui nodi edge, puoi [contaminare i nodi edge](/docs/containers?topic=containers-edge#edge_workloads). In Kubernetes versione 1.14 e successive, puoi distribuire gli NLB e gli ALB sia pubblici che privati ai nodi edge.
Ad esempio, se i tuoi nodi di lavoro sono connessi solo a una VLAN privata, ma ha bisogno di consentire l'accesso pubblico a un'applicazione nel tuo cluster, puoi creare un pool di nodi di lavoro edge in cui i nodi edge siano connessi alle VLAN pubbliche e private. Puoi distribuire gli NLB e gli ALB pubblici su questi nodi edge per garantire che solo quei nodi di lavoro gestiscano le connessioni pubbliche.

Se i tuoi nodi di lavoro sono connessi solo a una VLAN privata e utilizzi un dispositivo gateway per fornire la comunicazione tra i nodi di lavoro e il master cluster, puoi inoltre configurare il dispositivo come firewall pubblico o privato. Per consentire le richieste di traffico pubblico o privato dall'esterno del cluster alle tue applicazioni, puoi creare NodePort, NLB e ALB Ingress pubblici o privati. Quindi, devi [aprire le porte e gli indirizzi IP richiesti](/docs/containers?topic=containers-firewall#firewall_inbound) nel firewall del tuo dispositivo gateway per consentire il traffico in entrata verso questi servizi sulla rete pubblica o privata.
{: note}

<br />


## Scenario: Esegui carichi di lavoro dell'applicazione con connessione Internet in un cluster
{: #internet-facing}

In questo scenario, vuoi eseguire dei carichi di lavoro in un cluster che siano accessibili alle richieste da Internet in modo che gli utenti finali possano accedere alle tue applicazioni. Vuoi avere la possibilità di isolare l'accesso pubblico nel tuo cluster e di controllare quali richieste pubbliche sono consentite al cluster. Inoltre, i tuoi nodi di lavoro hanno accesso automatico a tutti i servizi {{site.data.keyword.cloud_notm}} che desideri connettere al tuo cluster.
{: shortdesc}

<p>
<figure>
 <img src="images/cs_clusters_planning_internet.png" alt="Immagine dell'architettura per un cluster che esegue carichi di lavoro con connessione Internet"/>
 <figcaption>Architettura per un cluster che esegue carichi di lavoro con connessione Internet</figcaption>
</figure>
</p>

Per ottenere questa configurazione, crei un cluster connettendo i nodi di lavoro alle VLAN pubbliche e private.

Se crei il cluster con VLAN pubbliche e private, non puoi rimuovere in seguito tutte le VLAN pubbliche da quel cluster. In caso di rimozione di tutte le VLAN pubbliche da un cluster, diversi componenti cluster smettono di funzionare. Crea invece un nuovo pool di nodi di lavoro che sia connesso solo a una VLAN privata.
{: note}

Puoi scegliere di consentire le comunicazioni tra nodo di lavoro e master e tra utente e master sulle reti pubbliche e private o solo sulla rete pubblica.
* Endpoint del servizio pubblico e privato: il tuo account deve essere abilitato con VRF e abilitato per utilizzare gli endpoint del servizio. Le comunicazioni tra i nodi di lavoro e il master vengono stabilite sia sulla rete privata attraverso l'endpoint del servizio privato che sulla rete pubblica attraverso l'endpoint del servizio pubblico. Il master è pubblicamente accessibile agli utenti del cluster autorizzati attraverso l'endpoint del servizio pubblico.
* Endpoint del servizio pubblico: se non vuoi o non puoi abilitare VRF per il tuo account, i tuoi nodi di lavoro e gli utenti del cluster autorizzati possono connettersi automaticamente al master Kubernetes sulla rete pubblica attraverso l'endpoint del servizio pubblico.

I tuoi nodi di lavoro possono comunicare in modo automatico e sicuro con altri servizi {{site.data.keyword.cloud_notm}} che supportano gli endpoint del servizio privato sulla tua rete privata dell'infrastruttura IBM Cloud. Se un servizio {{site.data.keyword.cloud_notm}} non supporta gli endpoint del servizio privato, i nodi di lavoro possono comunicare in modo sicuro con i servizi sulla rete pubblica. Puoi bloccare le interfacce pubbliche o private dei nodi di lavoro utilizzando le politiche di rete Calico per l'isolamento della rete pubblica o della rete privata. Potresti dover consentire l'accesso agli indirizzi IP pubblici e privati dei servizi che vuoi utilizzare in queste politiche di isolamento Calico.

Per esporre un'applicazione nel tuo cluster a Internet, puoi creare un servizio NLB (network load balancer) o ALB (application load balancer) Ingress pubblico. Puoi migliorare la sicurezza del tuo cluster creando un pool di nodi di lavoro etichettati come nodi edge. I pod per i servizi di rete pubblica vengono distribuiti sui nodi edge in modo che i carichi di lavoro del traffico esterno siano isolati solo a pochi nodi di lavoro nel cluster. Puoi controllare ulteriormente il traffico pubblico verso i servizi di rete che espongono le tue applicazioni creando delle politiche pre-DNAT Calico, come le politiche di whitelist e blacklist.

Se i tuoi nodi di lavoro devono accedere a servizi nelle reti private al di fuori del tuo account {{site.data.keyword.cloud_notm}}, puoi configurare e distribuire il servizio VPN IPSec strongSwan nel tuo cluster o sfruttare i servizi {{site.data.keyword.cloud_notm}} {{site.data.keyword.cloud_notm}} Direct Link per connetterti a queste reti.

Sei pronto a iniziare a usare un cluster per questo scenario? Dopo aver pianificato le tue configurazioni di [alta disponibilità](/docs/containers?topic=containers-ha_clusters) e dei [nodi di lavoro](/docs/containers?topic=containers-planning_worker_nodes), vedi [Creazione dei cluster](/docs/containers?topic=containers-clusters#cluster_prepare).

<br />


## Scenario: estendi il tuo data center in loco a un cluster sulla rete privata e aggiungi un accesso pubblico limitato
{: #limited-public}

In questo scenario, vuoi eseguire dei carichi di lavoro in un cluster che siano accessibili a servizi, database o altre risorse nel tuo data center in loco. Tuttavia, potresti dover fornire un accesso pubblico limitato al tuo cluster e voler garantire che qualsiasi accesso pubblico sia controllato e isolato nel cluster. Ad esempio, potresti aver bisogno che i tuoi nodi di lavoro accedano a un servizio {{site.data.keyword.cloud_notm}} che non supporta gli endpoint del servizio privato e che si debba accedere tramite la rete pubblica. Oppure, potresti dover fornire l'accesso pubblico limitato a un'applicazione che viene eseguita nel tuo cluster.
{: shortdesc}

Per ottenere questa configurazione cluster, puoi creare un firewall [utilizzando i nodi edge e le politiche di rete Calico](#calico-pc) o [utilizzando un dispositivo gateway](#vyatta-gateway).

### Utilizzo dei nodi edge e delle politiche di rete Calico
{: #calico-pc}

Consenti una connettività pubblica limitata al tuo cluster utilizzando i nodi edge come gateway pubblico e le politiche di rete Calico come firewall pubblico.
{: shortdesc}

<p>
<figure>
 <img src="images/cs_clusters_planning_calico.png" alt="Immagine dell'architettura per un cluster che utilizza nodi edge e politiche di rete Calico per un accesso pubblico sicuro"/>
 <figcaption>Architettura per un cluster che utilizza nodi edge e politiche di rete Calico per un accesso pubblico sicuro</figcaption>
</figure>
</p>

Con questa configurazione, crei un cluster connettendo i nodi di lavoro solo a una VLAN privata. Il tuo account deve essere abilitato con VRF e abilitato per utilizzare gli endpoint del servizio privato.

Il master OpenShift è accessibile tramite l'endpoint del servizio privato se gli utenti del cluster autorizzati si trovano nella tua rete privata {{site.data.keyword.cloud_notm}} o sono connessi alla rete privata tramite una [connessione VPN](/docs/infrastructure/iaas-vpn?topic=VPN-getting-started) o [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link). Tuttavia, le comunicazioni con il master Kubernetes sull'endpoint del servizio privato devono passare attraverso l'intervallo di indirizzi IP <code>166.X.X.X</code>, che non è instradabile da una connessione VPN o tramite {{site.data.keyword.cloud_notm}} Direct Link. Puoi esporre l'endpoint del servizio privato del master per gli utenti del tuo cluster utilizzando un NLB (network load balancer) privato. L'NLB privato espone l'endpoint del servizio privato del master come intervallo di indirizzi IP <code>10.X.X.X</code> interno a cui gli utenti possono accedere con la connessione VPN o {{site.data.keyword.cloud_notm}} Direct Link. Se abiliti solo l'endpoint del servizio privato, puoi utilizzare il dashboard Kubernetes o abilitare temporaneamente l'endpoint del servizio pubblico per creare l'NLB privato.

Successivamente, puoi creare un pool di nodi di lavoro connessi alle VLAN pubbliche e private ed etichettati come nodi edge. I nodi edge possono migliorare la sicurezza del tuo cluster consentendo solo a pochi nodi di lavoro di essere accessibili esternamente e isolando il carico di lavoro della rete a questi nodi di lavoro.

I tuoi nodi di lavoro possono comunicare in modo automatico e sicuro con altri servizi {{site.data.keyword.cloud_notm}} che supportano gli endpoint del servizio privato sulla tua rete privata dell'infrastruttura IBM Cloud. Se un servizio {{site.data.keyword.cloud_notm}} non supporta gli endpoint del servizio privato, i tuoi nodi edge che sono connessi a una VLAN pubblica possono comunicare in modo sicuro con i servizi sulla rete pubblica. Puoi bloccare le interfacce pubbliche o private dei nodi di lavoro utilizzando le politiche di rete Calico per l'isolamento della rete pubblica o della rete privata. Potresti dover consentire l'accesso agli indirizzi IP pubblici e privati dei servizi che vuoi utilizzare in queste politiche di isolamento Calico.

Per fornire l'accesso privato a un'applicazione nel tuo cluster, puoi creare un NLB (network load balancer) o un ALB (application load balancer) Ingress privato per esporre l'applicazione solo alla rete privata. Puoi bloccare tutto il traffico pubblico verso questi servizi di rete che espongono le tue applicazioni creando delle politiche pre-DNAT Calico, come le politiche per bloccare le NodePort pubbliche sui nodi di lavoro. Se hai bisogno di fornire un accesso pubblico limitato a un'applicazione nel tuo cluster, puoi creare un NLB o un ALB pubblico per esporre la tua applicazione. Devi quindi distribuire le tue applicazioni su questi nodi edge in modo che gli NLB o gli ALB possano indirizzare il traffico pubblico ai pod delle applicazioni. Puoi controllare ulteriormente il traffico pubblico verso i servizi di rete che espongono le tue applicazioni creando delle politiche pre-DNAT Calico, come le politiche di whitelist e blacklist. I pod per i servizi di rete sia pubblica che privata vengono distribuiti sui nodi edge in modo che i carichi di lavoro del traffico esterno siano limitati solo a pochi nodi di lavoro nel cluster.  

Per accedere in modo sicuro a servizi esterni a {{site.data.keyword.cloud_notm}} e ad altre reti in loco, puoi configurare e distribuire il servizio VPN IPSec strongSwan nel tuo cluster. Il pod del programma di bilanciamento del carico strongSwan viene distribuito su un nodo di lavoro nel pool edge, dove il pod stabilisce una connessione sicura alla rete in loco tramite un tunnel VPN crittografato sulla rete pubblica. In alternativa, puoi utilizzare i servizi {{site.data.keyword.cloud_notm}} Direct Link per connettere il tuo cluster al data center in loco solo sulla rete privata.

Sei pronto a iniziare a usare un cluster per questo scenario? Dopo aver pianificato le tue configurazioni di [alta disponibilità](/docs/containers?topic=containers-ha_clusters) e dei [nodi di lavoro](/docs/containers?topic=containers-planning_worker_nodes), vedi [Creazione dei cluster](/docs/containers?topic=containers-clusters#cluster_prepare).

</br>

### Utilizzo di un dispositivo gateway
{: #vyatta-gateway}

Consenti una connettività pubblica limitata al tuo cluster configurando un dispositivo gateway, ad esempio un Virtual Router Appliance (Vyatta), come gateway e firewall pubblico.
{: shortdesc}

<p>
<figure>
 <img src="images/cs_clusters_planning_gateway.png" alt="Immagine dell'architettura per un cluster che utilizza un dispositivo gateway per un accesso pubblico sicuro"/>
 <figcaption>Architettura per un cluster che utilizza un dispositivo gateway per un accesso pubblico sicuro</figcaption>
</figure>
</p>

Se configuri i tuoi nodi di lavoro solo su una VLAN privata e non vuoi o non puoi abilitare VRF per il tuo account, devi configurare un dispositivo gateway per fornire la connettività di rete tra i nodi di lavoro e il master sulla rete pubblica. Ad esempio, potresti scegliere di configurare un [Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-about-the-vra) o un [Fortigate Security Appliance](/docs/services/vmwaresolutions/services?topic=vmware-solutions-fsa_considerations).

Puoi configurare il tuo dispositivo gateway con politiche di rete personalizzate per fornire la sicurezza di rete dedicata per il tuo cluster e per rilevare e risolvere intrusioni di rete. Quando configuri un firewall sulla rete pubblica, devi aprire le porte e gli indirizzi IP privati richiesti per ogni regione in modo che il master e i nodi di lavoro possano comunicare. Se configuri questo firewall anche per la rete privata, devi aprire anche le porte e gli indirizzi IP privati necessari per consentire le comunicazioni tra i nodi di lavoro e permettere al tuo cluster di accedere alle risorse dell'infrastruttura sulla rete privata. Devi inoltre abilitare lo spanning della VLAN per il tuo account in modo che le sottoreti possano essere instradate sulla stessa VLAN e su tutte le VLAN.

Per connettere in modo sicuro i tuoi nodi di lavoro e le tue applicazioni a una rete in loco o a servizi esterni a {{site.data.keyword.cloud_notm}}, configura un endpoint VPN IPSec sul tuo dispositivo gateway e il servizio VPN IPSec strongSwan nel tuo cluster per utilizzare l'endpoint VPN del gateway. Se non vuoi utilizzare strongSwan, puoi configurare la connettività VPN direttamente con VRA.

I tuoi nodi di lavoro possono comunicare in modo sicuro con altri servizi {{site.data.keyword.cloud_notm}} e servizi pubblici esterni a {{site.data.keyword.cloud_notm}} tramite il tuo dispositivo gateway. Puoi configurare il tuo firewall per consentire l'accesso agli indirizzi IP pubblici e privati dei soli servizi che vuoi utilizzare.

Per fornire l'accesso privato a un'applicazione nel tuo cluster, puoi creare un NLB (network load balancer) o un ALB (application load balancer) Ingress privato per esporre l'applicazione solo alla rete privata. Se hai bisogno di fornire un accesso pubblico limitato a un'applicazione nel tuo cluster, puoi creare un NLB o un ALB pubblico per esporre la tua applicazione. Poiché tutto il traffico passa attraverso il firewall del tuo dispositivo gateway, puoi controllare il traffico pubblico e privato verso i servizi di rete che espongono le tue applicazioni aprendo le porte e gli indirizzi IP del servizio nel tuo firewall per consentire il traffico in entrata verso questi servizi.

Sei pronto a iniziare a usare un cluster per questo scenario? Dopo aver pianificato le tue configurazioni di [alta disponibilità](/docs/containers?topic=containers-ha_clusters) e dei [nodi di lavoro](/docs/containers?topic=containers-planning_worker_nodes), vedi [Creazione dei cluster](/docs/containers?topic=containers-clusters#cluster_prepare).

<br />


## Scenario: estendi il tuo data center in loco a un cluster sulla rete privata
{: #private_clusters}

In questo scenario, vuoi eseguire dei carichi di lavoro in un cluster {{site.data.keyword.containerlong_notm}}. Tuttavia, vuoi che questi carichi di lavoro siano accessibili solo a servizi, database o altre risorse nel tuo data center in loco, ad esempio {{site.data.keyword.icpfull_notm}}. I carichi di lavoro del tuo cluster potrebbero dover accedere ad alcuni altri servizi {{site.data.keyword.cloud_notm}} che supportano le comunicazioni sulla rete privata, ad esempio {{site.data.keyword.cos_full_notm}}.
{: shortdesc}

<p>
<figure>
 <img src="images/cs_clusters_planning_extend.png" alt="Immagine dell'architettura per un cluster che si connette a un data center in loco sulla rete privata"/>
 <figcaption>Architettura per un cluster che si connette a un data center in loco sulla rete privata</figcaption>
</figure>
</p>

Per ottenere questa configurazione, crei un cluster connettendo i nodi di lavoro solo a una VLAN privata. Per fornire la connettività tra il master cluster e i nodi di lavoro sulla rete privata solo tramite l'endpoint del servizio privato, il tuo account deve essere abilitato con VRF e abilitato per utilizzare gli endpoint del servizio. Poiché il tuo cluster è visibile a qualsiasi risorsa sulla rete privata quando VRF è abilitato, puoi isolare il tuo cluster da altri sistemi sulla rete privata applicando le politiche di rete privata Calico.

Il master OpenShift è accessibile tramite l'endpoint del servizio privato se gli utenti del cluster autorizzati si trovano nella tua rete privata {{site.data.keyword.cloud_notm}} o sono connessi alla rete privata tramite una [connessione VPN](/docs/infrastructure/iaas-vpn?topic=VPN-getting-started) o [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link). Tuttavia, le comunicazioni con il master Kubernetes sull'endpoint del servizio privato devono passare attraverso l'intervallo di indirizzi IP <code>166.X.X.X</code>, che non è instradabile da una connessione VPN o tramite {{site.data.keyword.cloud_notm}} Direct Link. Puoi esporre l'endpoint del servizio privato del master per gli utenti del tuo cluster utilizzando un NLB (network load balancer) privato. L'NLB privato espone l'endpoint del servizio privato del master come intervallo di indirizzi IP <code>10.X.X.X</code> interno a cui gli utenti possono accedere con la connessione VPN o {{site.data.keyword.cloud_notm}} Direct Link. Se abiliti solo l'endpoint del servizio privato, puoi utilizzare il dashboard Kubernetes o abilitare temporaneamente l'endpoint del servizio pubblico per creare l'NLB privato.

I tuoi nodi di lavoro possono comunicare in modo automatico e sicuro con altri servizi {{site.data.keyword.cloud_notm}} che supportano gli endpoint del servizio privato, come {{site.data.keyword.registrylong}}, sulla tua rete privata dell'infrastruttura IBM Cloud. Ad esempio, gli ambienti hardware dedicati per tutte le istanze del piano standard di {{site.data.keyword.cloudant_short_notm}} supportano gli endpoint del servizio privato. Se un servizio {{site.data.keyword.cloud_notm}} non supporta gli endpoint del servizio privato, il tuo cluster non può accedere a tale servizio.

Per fornire l'accesso privato a un'applicazione nel tuo cluster, puoi creare un NLB (network load balancer) o un ALB (application load balancer) Ingress privato. Questi servizi di rete Kubernetes espongono la tua applicazione solo alla rete privata in modo che qualsiasi sistema in loco con una connessione alla sottorete su cui si trova l'IP NLB possa accedere all'applicazione.

Sei pronto a iniziare a usare un cluster per questo scenario? Dopo aver pianificato le tue configurazioni di [alta disponibilità](/docs/containers?topic=containers-ha_clusters) e dei [nodi di lavoro](/docs/containers?topic=containers-planning_worker_nodes), vedi [Creazione dei cluster](/docs/containers?topic=containers-clusters#cluster_prepare).


