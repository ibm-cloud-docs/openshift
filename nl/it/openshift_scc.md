---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, scc, security context constraint, psp

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


# Configurazione dei vincoli del contesto di sicurezza
{: #openshift_scc}

Con i vincoli del contesto di sicurezza (o SCC, security context constraint), puoi controllare le azioni e l'accesso che può essere eseguito dai pod all'interno del tuo cluster {{site.data.keyword.openshiftlong}}. Per ulteriori informazioni sui SCC, vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).
{: shortdesc}

**Perché imposto i vincoli del contesto di sicurezza?**</br>
Come amministratore cluster, vuoi controllare cosa succede nel tuo cluster, specialmente le azioni che influiscono sulla sicurezza o sulla disponibilità del cluster. I vincoli del contesto di sicurezza possono aiutarti a controllare quali azioni e quale accesso sono disponibili per i pod nel tuo contenitore, come ad esempio l'utilizzo di contenitori privilegiati, di spazi dei nomi root, di reti host e di porte, di tipi di volume, di file system host, di autorizzazioni Linux come ID di gruppo o di sola lettura e altro.

Stai provando a controllare quali utenti hanno accesso al tuo cluster? Vedi [Assegnazione dell'accesso al cluster](/docs/openshift?topic=containers-users) per impostare le autorizzazioni {{site.data.keyword.cloud_notm}} IAM e dell'infrastruttura.
{: tip}

**Ci sono SCC configurati per impostazione predefinita?**</br>
Per impostazione predefinita, i cluster Red Hat OpenShift on IBM Cloud includono una serie standard di [SCC OpenShift](#oc_sccs). Inoltre, i cluster hanno degli [SCC IBM](#ibm_sccs) che assomigliano molto alle [politiche della sicurezza di pod Kubernetes dei cluster Kubernetes della community in {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-psp#ibm_psp). Questi SCC IBM sono inclusi per una portabilità migliorata con i pacchetti privati {{site.data.keyword.cloud_notm}} come i Cloud Pak.

**Posso utilizzare invece le politiche di sicurezza dei pod Kubernetes?**</br>
No. [Le politiche di sicurezza pod (o PSP, pod security policy) Kubernetes ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/policy/pod-security-policy/) sono basate originariamente sui vincoli del contesto di sicurezza (o SCC, Security Context Constraint) OpenShift. Tuttavia, OpenShift 3.11 supporta solo gli SCC, non le PSP.

Gli SCC OpenShift predefiniti sono più rigidi delle PSP predefinite nei cluster Kubernetes della community. Pertanto, le distribuzioni di applicazioni che vengono eseguite nei cluster Kubernetes della community potrebbero dover essere modificate per l'esecuzione in OpenShift.

<br />


## Personalizzazione dei vincoli del contesto di sicurezza (o SCC, Security Context Constraint) 
{: #customize_sccs}

Per creare, modificare, elencare, eliminare e in altro modo gestire i vincoli del contesto di sicurezza (o SCC, Security Context Constraint), vedi la [documentazione di OpenShift ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html). Puoi anche aggiungere utenti o gruppi ai vincoli del contesto di sicurezza (o SCC, Security Context Constraint) predefiniti
{: shortdesc}

<br />


## Vincoli del contesto di sicurezza OpenShift predefiniti
{: #oc_sccs}

I cluster Red Hat OpenShift on IBM Cloud vengono forniti, per impostazione predefinita, con i seguenti vincoli del contesto di sicurezza (o SCC, Security Context Constraint).
{: shortdesc}

Non modificare le impostazioni di SCC IBM od OpenShift, fatta eccezione per i campi `priority`, `users` o `groups`.
{: note}

|Nome SCC | Descrizione |
|---------|-------------|
| `anyuid`| Nega l'accesso in modo analogo all'SCC `restricted` ma consente l'esecuzione degli utenti con qualsiasi UID e GID.|
| `hostaccess`| Consente l'accesso a tutti gli spazi dei nomi host ma richiede comunque che i pod siano eseguiti con un UID e un contesto SELinux che sono assegnati allo spazio dei nomi. <p class="important">Concedi questo SCC solo per i pod attendibili che richiedono l'accesso host a spazi dei nomi, file system e PID (process ID).</p>|
| `hostmount-anyuid` | Nega l'accesso in modo analogo all'SCC `restricted` ma consente il montaggio host e qualsiasi UID da un pod. Questo SCC viene utilizzato principalmente dal riciclatore di volumi persistenti. <p class="important">Concedi questo SCC solo per i pod che richiedono l'accesso al file system host come qualsiasi UID, compreso l'UID 0.</p>|
| `hostnetwork`| Consente l'utilizzo di rete host e porte host ma richiede comunque che i pod siano eseguiti con un UID e un contesto SELinux che sono assegnati allo spazio dei nomi.<p class="important">Concedi questo SCC solo per i pod che richiedono l'accesso di rete host.</p>|
| `node-exporter`| Concede l'accesso appropriato per l'esportatore di nodi Prometheus integrato. |
| `nonroot`| Nega l'accesso in modo analogo all'SCC `restricted` ma consente l'esecuzione degli utenti con qualsiasi UID non root. L'utente o il manifest del runtime del contenitore devono specificare l'UID.|
| `privileged`| Consente l'accesso a tutte le funzioni privilegiate e host e la capacità di esecuzione come qualsiasi utente, gruppo e fsGroup e con qualsiasi contesto SELinux.<p class="important">Concedi questo SCC solo per l'amministrazione del cluster che richiede il massimo accesso possibile.</p>|
| `restricted`| Nega l'accesso a tutte le funzioni host e richiede che i pod siano eseguiti con un UID e un contesto SELinux che sono assegnati allo spazio dei nomi. Questo è l'SCC più restrittivo e viene utilizzato per impostazione predefinita per gli utenti autenticati.|
{: caption="Vincoli del contesto di sicurezza OpenShift predefiniti" caption-side="top"}

<br />


## Vincoli del contesto di sicurezza IBM predefiniti
{: #ibm_sccs}

I cluster Red Hat OpenShift on IBM Cloud vengono forniti, per impostazione predefinita, con i seguenti vincoli del contesto di sicurezza (o SCC, Security Context Constraint) IBM.
{: shortdesc}

Non modificare le impostazioni di SCC IBM od OpenShift, fatta eccezione per i campi `priority`, `users` o `groups`.
{: note}

|Nome SCC | Descrizione |
|---------|-------------|
| `ibm-anyuid-hostaccess-scc`| Consente l'esecuzione dei pod con qualsiasi UID e GID, qualsiasi volume e l'accesso completo all'host.<p class="important">Concedi questo SCC solo per i pod che richiedono l'accesso completo all'host e alla rete.</p>|
| `ibm-anyuid-hostpath-scc`| Consente l'esecuzione dei pod con qualsiasi UID e GID e qualsiasi volume, compreso il percorso host.<p class="important">Concedi questo SCC solo per i pod che richiedono l'accesso ai volumi `hostPath`.</p>|
| `ibm-anyuid-scc` | Consente l'esecuzione dei pod con qualsiasi UID e GID ma impedisce l'accesso all'host.|
| `ibm-privileged-scc`| Concede l'accesso a tutte le funzioni host privilegiate e consente l'esecuzione di un pod con qualsiasi UID e GID e qualsiasi volume.<p class="important">Concedi questo SCC solo per l'amministrazione del cluster che richiede il massimo accesso possibile.</p> |
{: caption="Vincoli del contesto di sicurezza IBM predefiniti" caption-side="top"}
