---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, compliance, security standards

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

# Architettura del servizio
{: #openshift-service-arch}

Il diagramma e la tabella che seguono descrivono i componenti predefiniti che sono configurati in un'architettura {{site.data.keyword.openshiftlong}}.
{: shortdesc}

Per ulteriori informazioni sull'architettura di OpenShift Container Platform, vedi la [documentazione di OpenShift![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/architecture/index.html).
{: note}

![Architettura del cluster Red Hat OpenShift on IBM Cloud](/images/cs_org_ov_both_ses_rhos.png)

Scorri la seguente tabella per ulteriori informazioni sui componenti di nodo di lavoro e master cluster.

| Componenti master| Descrizione |
|:-----------------|:-----------------|
| Repliche | I componenti master, tra cui il server API Kubernetes e l'archivio dati etcd di OpenShift, hanno tre repliche e, se situati in un'area metropolitana multizona, vengono estesi tra le zone per una disponibilità ancora maggiore. I componenti master vengono sottoposti a backup ogni 8 ore.|
| `rhos-api` | Il server API Kubernetes di OpenShift funge da punto di ingresso principale per tutte le richieste di gestione del cluster dal nodo di lavoro al master. Il server API convalida ed elabora le richieste che modificano lo stato delle risorse Kubernetes, come i pod o i servizi, e archivia questo stato nell'archivio dati etcd.|
| `openvpn-server` | Il server OpenVPN funziona con il client OpenVPN per connettere in modo protetto il master al nodo di lavoro. Questa connessione supporta le chiamate `apiserver proxy` ai tuoi pod e servizi e le chiamate `oc exec`, `attach` e `logs` a kubelet.|
| `etcd` | etcd è un archivio di valori chiave altamente disponibile che archivia lo stato di tutte le risorse Kubernetes di un cluster, quali servizi, distribuzioni e pod. I dati in etcd sono sottoposti a backup su un'istanza di archiviazione crittografata gestita da IBM.|
| `rhos-controller` | Il gestore controller OpenShift verifica i pod appena creati e decide dove distribuirli in base a capacità, esigenze di prestazioni, vincoli delle politiche, specifiche di anti-affinità e requisiti del carico di lavoro. Se non è possibile trovare alcun nodo di lavoro che corrisponda ai requisiti, il pod non viene distribuito nel cluster. Il controller verifica anche lo stato delle risorse del cluster, come le serie di repliche. Quando lo stato di una risorsa viene modificato, ad esempio se si verifica un'interruzione di un pod in una serie di repliche, il gestore controller avvia le azioni correttive per raggiungere lo stato richiesto. `rhos-controller` funziona sia come programma di pianificazione (scheduler) che come gestore controller in una configurazione Kubernetes della community. |
| `cloud-controller-manager` | Il gestore controller cloud gestisce i componenti specifici del provider cloud, come ad esempio il programma di bilanciamento del carico {{site.data.keyword.cloud_notm}}.|
| Controller di ammissione |I controller di ammissione sono implementati per specifiche funzioni in OpenShift e {{site.data.keyword.containerlong_notm}}. Con i controller di ammissione, puoi configurare le politiche nel tuo cluster che determinano se una specifica azione nel cluster è consentita o meno. Nella politica, puoi specificare le condizioni quando un utente non può eseguire un'azione, anche se tale azione fa parte delle autorizzazioni generali da te assegnate all'utente utilizzando RBAC. Pertanto, i controller di ammissione possono fornire un livello supplementare di sicurezza per il tuo cluster prima che una richiesta API venga elaborata dal server API Kubernetes. </br></br> Quando crei un cluster OpenShift, {{site.data.keyword.containerlong_notm}} installa automaticamente i seguenti [controller di ammissione Kubernetes![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/admin/admission-controllers/) nell'ordine indicato nel master Kubernetes, che non può essere modificato dall'utente:<ul><li>`NamespaceLifecycle`</li><li>`LimitRanger`</li><li>`ServiceAccount`</li><li>`DefaultStorageClass`</li><li>`ResourceQuota`</li><li>`StorageObjectInUseProtection`</li><li>`PersistentVolumeClaimResize`</li><li>[`Priority`](/docs/containers?topic=containers-pod_priority#pod_priority)</li><li>`BuildByStrategy`</li><li>`OriginPodNodeEnvironment`</li><li>`PodNodeSelector`</li><li>`ExternalIPRanger`</li><li>`NodeRestriction`</li><li>`SecurityContextConstraint`</li><li>`SCCExecRestrictions`</li><li>`PersistentVolumeLabel`</li><li>`OwnerReferencesPermissionEnforcement`</li><li>`PodTolerationRestriction`</li><li>`openshift.io/JenkinsBootstrapper`</li><li>`openshift.io/BuildConfigSecretInjector`</li><li>`openshift.io/ImageLimitRange`</li><li>`openshift.io/RestrictedEndpointsAdmission`</li><li>`openshift.io/ImagePolicy`</li><li>`openshift.io/IngressAdmission`</li><li>`openshift.io/ClusterResourceQuota`</li><li>`MutatingAdmissionWebhook`</li><li>`ValidatingAdmissionWebhook`</li></ul></br><p>Puoi [installare i tuoi controller di ammissione nel cluster ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks) o scegliere dai controller di ammissione facoltativi forniti da {{site.data.keyword.containerlong_notm}}. </p><ul><li><strong>[Container Image Security Enforcer](/docs/services/Registry?topic=registry-security_enforce#security_enforce):</strong> utilizza questo controller di ammissione per implementare le politiche del Controllo vulnerabilità nel tuo cluster per bloccare le distribuzioni da immagini vulnerabili.</li></ul></br><p class="note">Se hai installato manualmente i controller di ammissione e non vuoi più usarli, assicurati di rimuoverli completamente. Se i controller di ammissione non vengono rimossi completamente, potrebbero bloccare tutte le azioni che vuoi eseguire sul cluster.</p>
{: caption="Tabella 1. Componenti master OpenShift." caption-side="top"}
{: #rhos-components-1}
{: tab-title="Master"}
{: tab-group="rhos-components"}
{: class="simple-tab-table"}

| Componenti di nodo di lavoro| Descrizione |
|:-----------------|:-----------------|
| Sistema operativo | I nodi di lavoro Red Hat OpenShift on IBM Cloud vengono eseguiti sul sistema operativo Red Hat Enterprise Linux 7. |
| Progetti | OpenShift organizza le tue risorse in progetti, che sono spazi dei nomi Kubernetes con annotazioni, e include molti più componenti rispetto ai cluster Kubernetes della community per eseguire funzioni OpenShift come il catalogo. I componenti selezionati dei progetti sono descritti nelle seguenti righe. Per ulteriori informazioni, vedi [Progetti e utenti ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/architecture/core_concepts/projects_and_users.html).|
| `kube-system` | Questo spazio dei nomi include molti componenti che vengono utilizzati per eseguire Kubernetes sul nodo di lavoro.<ul><li>**`ibm-master-proxy`**: `ibm-master-proxy` è una serie di daemon che inoltra le richieste dal nodo di lavoro agli indirizzi IP delle repliche master altamente disponibili. Nei cluster a zona singola, il master ha tre repliche su host separati. Per i cluster che si trovano in una zona che supporta il multizona, il master ha tre repliche che vengono distribuite tra le zone. Un programma di bilanciamento del carico altamente disponibile inoltra le richieste effettuate al nome di dominio del master alle repliche del master.</li><li>**`openvpn-client`**: il client OpenVPN funziona con il server OpenVPN per connettere in modo protetto il master al nodo di lavoro. Questa connessione supporta le chiamate `apiserver proxy` ai tuoi pod e servizi e le chiamate `oc exec`, `attach` e `logs` a kubelet.</li><li>**`kubelet`**: kubelet è un agent del nodo di lavoro che viene eseguito su ogni nodo di lavoro ed è responsabile del monitoraggio dell'integrità dei pod in esecuzione sul nodo di lavoro e del controllo degli eventi inviati dal server API Kubernetes. In base agli eventi, il kubelet crea o rimuove i pod, garantisce i probe di attività e disponibilità e segnala in risposta lo stato dei pod al server API Kubernetes.</li><li>**`calico`**: Calico gestisce le politiche di rete per il tuo cluster e include alcuni componenti per gestire la connettività di rete dei contenitori, l'assegnazione di indirizzi IP e il controllo del traffico di rete.</li><li>**Altri componenti**: lo spazio dei nomi `kube-system` include anche dei componenti per gestire le risorse fornite da IBM come i plugin di archiviazione per l'archiviazione file e blocchi, l'ALB (application load balancer) ingress, la registrazione `fluentd` e `keepalived`.</li></ul>|
| `ibm-system` | Questo spazio dei nomi include la distribuzione `ibm-cloud-provider-ip` che funziona con `keepalived` per fornire il controllo dell'integrità e il bilanciamento del carico di livello 4 per le richieste ai pod dell'applicazione.|
| `kube-proxy-and-dns`| Questo spazio dei nomi include i componenti per convalidare il traffico di rete in entrata rispetto alle regole `iptables` configurate sul nodo di lavoro e le richieste di proxy che possono entrare o uscire dal cluster.|
| `default` | Questo spazio dei nomi viene utilizzato se non specifichi uno spazio dei nomi o crei un progetto per le tue risorse Kubernetes. Inoltre, lo spazio dei nomi predefinito include i seguenti componenti per supportare i tuoi cluster OpenShift.<ul><li>**`router`**: OpenShift utilizza gli [instradamenti ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html) per esporre il servizio di un'applicazione su un nome host in modo che i client esterni possano raggiungere il servizio. Il router associa il servizio al nome host.</li><li>**`docker-registry`** e **`registry-console`**: OpenShift fornisce un [registro di immagini contenitore ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html) interno che puoi utilizzare per gestire e visualizzare localmente le immagini attraverso la console. In alternativa puoi configurare l'{{site.data.keyword.registrylong_notm}} privato.</li></ul>|
| Altri progetti | Altri componenti sono installati in vari spazi dei nomi per impostazione predefinita per abilitare funzionalità come la registrazione, il monitoraggio e la console OpenShift.<ul><li><code>ibm-cert-store</code></li><li><code>kube-public</code></li><li><code>kube-service-catalog</code></li><li><code>openshift</code></li><li><code>openshift-ansible-service-broker</code></li><li><code>openshift-console</code></li><li><code>openshift-infra</code></li><li><code>openshift-monitoring</code></li><li><code>openshift-node</code></li><li><code>openshift-template-service-broker</code></li><li><code>openshift-web-console</code></li></ul>|
{: caption="Tabella 2. Componenti di nodo di lavoro OpenShift." caption-side="top"}
{: #rhos-components-2}
{: tab-title="Worker nodes"}
{: tab-group="rhos-components"}
{: class="simple-tab-table"}
