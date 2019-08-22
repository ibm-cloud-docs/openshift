---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, rhoks, roks, rhos, ibmcloud, ic, oc, ibmcloud oc

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

# CLI Red Hat OpenShift on IBM Cloud
{: #kubernetes-service-cli}

Fai riferimento a questi comandi per creare e gestire **entrambi i cluster Kubernetes o OpenShift della community** in {{site.data.keyword.containerlong}}.
{:shortdesc}

* **Kubernetes della community**: [Installa il plugin CLI](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps), che utilizza l'alias `ibmcloud ks`.
* **OpenShift**: [Installa il plugin CLI](/docs/openshift?topic=openshift-openshift-cli) che utilizza l'alias `ibmcloud oc`.

Nel terminale, ricevi una notifica quando sono disponibili degli aggiornamenti ai plugin e alla CLI `ibmcloud`. Assicurati di mantenere la tua CLI aggiornata in modo che tu possa utilizzare tutti i comandi e gli indicatori disponibili.

Cerchi i comandi `ibmcloud cr`? Consulta i [riferimenti CLI {{site.data.keyword.registryshort_notm}}](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli). Stai cercando i comandi `kubectl`? Consulta la [Documentazione Kubernetes ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubectl.docs.kubernetes.io/).
{:tip}

## Utilizzo del plugin beta {{site.data.keyword.containerlong_notm}}
{: #cs_beta}

Una versione riprogettata del plugin {{site.data.keyword.containerlong_notm}} è disponibile come beta. Il plugin {{site.data.keyword.containerlong_notm}} riprogettato raggruppa i comandi in categorie e modifica i comandi da una struttura con trattino a una struttura con spaziatura. Inoltre, a partire dalla versione beta `0.3` (valore predefinito), è disponibile una nuova [funzionalità di endpoint globale](/docs/containers?topic=containers-regions-and-zones#endpoint).
{: shortdesc}

Sono disponibili le seguenti versioni beta del plugin {{site.data.keyword.containerlong_notm}} riprogettato.
* La modalità di funzionamento predefinita è `0.3`. Assicurati che il tuo plug-in {{site.data.keyword.containerlong_notm}} utilizzi la versione `0.3` più recente eseguendo `ibmcloud plugin update kubernetes-service`.
* Per utilizzare `0.4` o `1.0`, imposta la variabile di ambiente `IKS_BETA_VERSION` alla versione beta che vuoi utilizzare:
    ```
    export IKS_BETA_VERSION=<beta_version>
    ```
    {: pre}
* Per utilizzare l'obsoleta funzionalità di endpoint regionale, indica come destinazione l'endpoint regionale con il [comando `init`](#cs_init).
    ```
    ibmcloud oc init --host <regional_endpoint>
    ```
    {: pre}

</br>

<table>
<caption>Versioni beta del plugin {{site.data.keyword.containerlong_notm}} riprogettato</caption>
  <thead>
    <th>Versione beta</th>
    <th>Struttura dell'output `ibmcloud oc help`</th>
    <th>Struttura del comando</th>
    <th>Funzionalità di ubicazione</th>
  </thead>
  <tbody>
    <tr>
      <td><code>0.2</code> (obsoleto)</td>
      <td>Legacy: i comandi sono mostrati nella struttura con trattino e sono elencati in ordine alfabetico.</td>
      <td>Legacy e beta: puoi eseguire i comandi nella struttura con trattino legacy (`ibmcloud oc alb-cert-get`) o nella struttura con spaziatura beta (`ibmcloud oc alb cert get`).</td>
      <td>Regionale: [Indica come destinazione una regione e utilizza un endpoint regionale per gestire le risorse in tale regione](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
    <tr>
      <td><code>0.3</code> (predefinito)</td>
      <td>Legacy: i comandi sono mostrati nella struttura con trattino e sono elencati in ordine alfabetico.</td>
      <td>Legacy e beta: puoi eseguire i comandi nella struttura con trattino legacy (`ibmcloud oc alb-cert-get`) o nella struttura con spaziatura beta (`ibmcloud oc alb cert get`).</td>
      <td>Globale: [Utilizza l'endpoint globale per gestire le risorse in qualsiasi ubicazione](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
    <tr>
      <td><code>0.4</code></td>
      <td>Beta: i comandi sono mostrati nella struttura con spaziatura e sono elencati in categorie.</td>
      <td>Legacy e beta: puoi eseguire i comandi nella struttura con trattino legacy (`ibmcloud oc alb-cert-get`) o nella struttura con spaziatura beta (`ibmcloud oc alb cert get`).</td>
      <td>Globale: [Utilizza l'endpoint globale per gestire le risorse in qualsiasi ubicazione](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
    <tr>
      <td><code>1.0</code></td>
      <td>Beta: i comandi sono mostrati nella struttura con spaziatura e sono elencati in categorie.</td>
      <td>Beta: puoi eseguire i comandi solo nella struttura con spaziatura beta (`ibmcloud oc alb cert get`).</td>
      <td>Globale: [Utilizza l'endpoint globale per gestire le risorse in qualsiasi ubicazione](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
  </tbody>
</table>



<br />


## Comandi API
{: #api_commands}

### `ibmcloud oc api`
{: #cs_cli_api}

Specifica l'endpoint API per {{site.data.keyword.containerlong_notm}}. Se non specifichi un endpoint, puoi visualizzare le informazioni sull'endpoint corrente che viene specificato.
{: shortdesc}

Gli endpoint specifici per la regione sono stati dichiarati obsoleti. Utilizza invece l'[endpoint globale](/docs/containers?topic=containers-regions-and-zones#endpoint). Se devi utilizzare gli endpoint regionali, [imposta la variabile di ambiente `IKS_BETA_VERSION` nel plug-in {{site.data.keyword.containerlong_notm}} su `0.2`](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_beta).
{: deprecated}

Se devi elencare e gestire le risorse solo da una singola regione, puoi utilizzare il comando `ibmcloud oc api` per indicare come destinazione un endpoint regionale invece dell'endpoint globale.
* Dallas (Stati Uniti Sud, us-south): `https://us-south.containers.cloud.ibm.com`
* Francoforte (Europa Centrale, eu-de): `https://eu-de.containers.cloud.ibm.com`
* Londra (Regno Unito Sud, eu-gb): `https://eu-gb.containers.cloud.ibm.com`
* Sydney (Asia Pacifico Sud, au-syd): `https://au-syd.containers.cloud.ibm.com`
* Tokyo (Asia Pacifico Nord, jp-tok): `https://jp-tok.containers.cloud.ibm.com`
* Washington, D.C. (Stati Uniti Est, us-east): `https://us-east.containers.cloud.ibm.com`

Per utilizzare la funzionalità globale, puoi utilizzare nuovamente il comando `ibmcloud oc api` per indicare come destinazione l'endpoint globale: `https://containers.cloud.ibm.com`

```
ibmcloud oc api --endpoint ENDPOINT [--insecure] [--skip-ssl-validation] [--api-version VALUE] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

**Opzioni comando**:
<dl>
<dt><code>--endpoint <em>ENDPOINT</em></code></dt>
  <dd>L'endpoint API {{site.data.keyword.containerlong_notm}}. <strong>Nota</strong>: questo endpoint è diverso dagli endpoint {{site.data.keyword.cloud_notm}}. Questo valore è obbligatorio per configurare l'endpoint API.
   </dd>

<dt><code>--insecure</code></dt>
<dd>Consente una connessione HTTP non sicura. Questo indicatore è facoltativo.</dd>

<dt><code>--skip-ssl-validation</code></dt>
<dd>Consente i certificati SSL non sicuri. Questo indicatore è facoltativo.</dd>

<dt><code>--api-version VALUE</code></dt>
<dd>Specifica la versione dell'API del servizio che vuoi utilizzare. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>

</dl>

**Esempio**: visualizza le informazioni sull'endpoint API corrente che viene specificato.
```
ibmcloud oc api
```
{: pre}

```
API Endpoint:          https://containers.cloud.ibm.com
API Version:           v1
Skip SSL Validation:   false
Region:                us-south
```
{: screen}

</br>
### `ibmcloud oc apiserver-refresh (cluster-refresh)`
{: #cs_apiserver_refresh}

Applica le modifiche di configurazione per il master Kubernetes che sono state richieste con i comandi `ibmcloud oc apiserver-config-set`, `apiserver-config-unset`, `cluster-feature-enable` o `cluster-feature-disable`. I componenti master Kubernetes altamente disponibili sono riavviati in un riavvio progressivo. I nodi di lavoro, le applicazioni e le risorse non vengono modificati e continuano l'esecuzione.
{: shortdesc}



```
ibmcloud oc apiserver-refresh --cluster CLUSTER [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

<br />


## Comandi utilizzo plugin CLI
{: #cli_plug-in_commands}

### `ibmcloud oc help`
{: #cs_help}

Visualizza un elenco di comandi e parametri supportati.
{: shortdesc}

```
ibmcloud oc help
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

**Opzioni comando**: nessuna

</br>
### `ibmcloud oc init`
{: #cs_init}

Inizializza il plugin {{site.data.keyword.containerlong_notm}} o specifica la regione in cui desideri creare o accedere ai cluster Kubernetes.
{: shortdesc}

Gli endpoint specifici per la regione sono stati dichiarati obsoleti. Utilizza invece l'[endpoint globale](/docs/containers?topic=containers-regions-and-zones#endpoint). Se devi utilizzare gli endpoint regionali, [imposta la variabile di ambiente `IKS_BETA_VERSION` nel plug-in {{site.data.keyword.containerlong_notm}} su `0.2`](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_beta).
{: deprecated}

Se devi elencare e gestire le risorse solo da una singola regione, puoi utilizzare il comando `ibmcloud oc init` per indicare come destinazione un endpoint regionale invece dell'endpoint globale.

* Dallas (Stati Uniti Sud, us-south): `https://us-south.containers.cloud.ibm.com`
* Francoforte (Europa Centrale, eu-de): `https://eu-de.containers.cloud.ibm.com`
* Londra (Regno Unito Sud, eu-gb): `https://eu-gb.containers.cloud.ibm.com`
* Sydney (Asia Pacifico Sud, au-syd): `https://au-syd.containers.cloud.ibm.com`
* Tokyo (Asia Pacifico Nord, jp-tok): `https://jp-tok.containers.cloud.ibm.com`
* Washington, D.C. (Stati Uniti Est, us-east): `https://us-east.containers.cloud.ibm.com`

Per utilizzare la funzionalità globale, puoi utilizzare nuovamente il comando `ibmcloud oc init` per indicare come destinazione l'endpoint globale: `https://containers.cloud.ibm.com`

```
ibmcloud oc init [--host HOST] [--insecure] [-p] [-u] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

**Opzioni comando**:
<dl>
<dt><code>--host <em>HOST</em></code></dt>
<dd>L'endpoint API {{site.data.keyword.containerlong_notm}} da utilizzare. Questo valore è facoltativo.</dd>

<dt><code>--insecure</code></dt>
<dd>Consente una connessione HTTP non sicura.</dd>

<dt><code>-p</code></dt>
<dd>La tua password IBM Cloud.</dd>

<dt><code>-u</code></dt>
<dd>Il tuo nome utente IBM Cloud.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>

</dl>

**Esempi**:
*  Esempio di indicazione dell'endpoint regionale Stati Uniti Sud:
  ```
  ibmcloud oc init --host https://us-south.containers.cloud.ibm.com
  ```
  {: pre}
*  Esempio per indicare nuovamente come destinazione l'endpoint globale:
  ```
  ibmcloud oc init --host https://containers.cloud.ibm.com
  ```
  {: pre}
</br>

### `ibmcloud oc messages`
{: #cs_messages}

Visualizza i messaggi correnti dal plug-in della CLI {{site.data.keyword.containerlong_notm}} per l'utente ID IBM.
{: shortdesc}

```
ibmcloud oc messages
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

<br />


## Comandi cluster: gestione
{: #cluster_mgmt_commands}

### `ibmcloud oc addon-versions`
{: #cs_addon_versions}

Visualizza un elenco di versioni supportate per i componenti aggiuntivi gestiti in {{site.data.keyword.containerlong_notm}}.
{: shortdesc}



```
ibmcloud oc addon-versions [--addon ADD-ON_NAME] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

**Opzioni comando**:
<dl>
<dt><code>--addon <em>ADD-ON_NAME</em></code></dt>
<dd>Facoltativo: specifica il nome di un componente aggiuntivo, quale <code>istio</code> o <code>knative</code>, per cui filtrare le versioni.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:

  ```
  ibmcloud oc addon-versions --addon istio
  ```
  {: pre}

</br>
### `ibmcloud oc cluster-addon-disable`
{: #cs_cluster_addon_disable}

Disabilita un componente aggiuntivo gestito in un cluster esistente. Questo comando deve essere combinato con uno dei seguenti comandi secondari per il componente aggiuntivo gestito che vuoi disabilitare.
{: shortdesc}





#### `ibmcloud oc cluster-addon-disable istio`
{: #cs_cluster_addon_disable_istio}

Disabilita il componente aggiuntivo Istio gestito. Rimuove tutti i componenti core di Istio dal cluster, incluso Prometheus.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable istio --cluster CLUSTER [-f]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>-f</code></dt>
<dd>Facoltativo: questo componente aggiuntivo Istio è una dipendenza per i componenti aggiuntivi gestiti <code>istio-extras</code>, <code>istio-sample-bookinfo</code> e <code>knative</code>. Includi questo indicatore per disabilitare anche questi componenti aggiuntivi.</dd>
</dl>

#### `ibmcloud oc cluster-addon-disable istio-extras`
{: #cs_cluster_addon_disable_istio_extras}

Disabilita il componente aggiuntivo dei supplementi Istio gestito. Rimuove Grafana, Jeager e Kiali dal cluster.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable istio-extras --cluster CLUSTER [-f]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>-f</code></dt>
<dd>Facoltativo: questo componente aggiuntivo Istio è una dipendenza per il componente aggiuntivo gestito <code>istio-sample-bookinfo</code>. Includi questo indicatore per disabilitare anche questo componente aggiuntivo.</dd>
</dl>

#### `ibmcloud oc cluster-addon-disable istio-sample-bookinfo`
{: #cs_cluster_addon_disable_istio_sample_bookinfo}

Disabilita il componente aggiuntivo BookInfo Istio gestito. Rimuove tutte le distribuzioni, i pod e altre risorse dell'applicazione BookInfo dal cluster.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable istio-sample-bookinfo --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>
</dl>

#### `ibmcloud oc cluster-addon-disable knative`
{: #cs_cluster_addon_disable_knative}

Disabilita il componente aggiuntivo Knative gestito per rimuovere il framework senza server Knative dal cluster.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable knative --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>
</dl>

#### `ibmcloud oc cluster-addon-disable kube-terminal`
{: #cs_cluster_addon_disable_kube-terminal}

Disabilita il componente aggiuntivo [Kubernetes Terminal](/docs/containers?topic=containers-cs_cli_install#cli_web). Per utilizzare il Kubernetes Terminal nella console del cluster {{site.data.keyword.containerlong_notm}}, devi prima riabilitare il componente aggiuntivo.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable kube-terminal --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>
</dl>

</br>

### `ibmcloud oc cluster-addon-enable`
{: #cs_cluster_addon_enable}

Abilita un componente aggiuntivo gestito in un cluster esistente. Questo comando deve essere combinato con uno dei seguenti comandi secondari per il componente aggiuntivo gestito che vuoi abilitare.
{: shortdesc}





#### `ibmcloud oc cluster-addon-enable istio`
{: #cs_cluster_addon_enable_istio}

Abilita il [componente aggiuntivo Istio](/docs/containers?topic=containers-istio) gestito. Installa i componenti core di Istio, incluso Prometheus.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable istio --cluster CLUSTER [--version VERSION]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Facoltativo: specifica la versione del componente aggiuntivo da installare. Se non viene specificata alcuna versione, viene installata quella predefinita.</dd>
</dl>

#### `ibmcloud oc cluster-addon-enable istio-extras`
{: #cs_cluster_addon_enable_istio_extras}

Abilita il componente aggiuntivo dei supplementi Istio gestito. Installa Grafana, Jeager e Kiali per offrire ulteriori funzioni di monitoraggio, traccia e visualizzazione per Istio.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable istio-extras --cluster CLUSTER [--version VERSION] [-y]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Facoltativo: specifica la versione del componente aggiuntivo da installare. Se non viene specificata alcuna versione, viene installata quella predefinita.</dd>

<dt><code>-y</code></dt>
<dd>Facoltativo: abilita la dipendenza del componente aggiuntivo <code>istio</code>.</dd>
</dl>

#### `ibmcloud oc cluster-addon-enable istio-sample-bookinfo`
{: #cs_cluster_addon_enable_istio_sample_bookinfo}

Abilita il componente aggiuntivo BookInfo Istio gestito. Distribuisce l'[applicazione di esempio BookInfo per Istio ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://istio.io/docs/examples/bookinfo/) nello spazio dei nomi di <code>default</code>.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable istio-sample-bookinfo --cluster CLUSTER [--version VERSION] [-y]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Facoltativo: specifica la versione del componente aggiuntivo da installare. Se non viene specificata alcuna versione, viene installata quella predefinita.</dd>

<dt><code>-y</code></dt>
<dd>Facoltativo: abilita le dipendenze del componente aggiuntivo <code>istio</code> e <code>istio-extras</code>.</dd>
</dl>

#### `ibmcloud oc cluster-addon-enable knative`
{: #cs_cluster_addon_enable_knative}

Abilita il [componente aggiuntivo Knative](/docs/containers?topic=containers-serverless-apps-knative) gestito per installare il framework senza server Knative.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable knative --cluster CLUSTER [--version VERSION] [-y]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Facoltativo: specifica la versione del componente aggiuntivo da installare. Se non viene specificata alcuna versione, viene installata quella predefinita.</dd>

<dt><code>-y</code></dt>
<dd>Facoltativo: abilita la dipendenza del componente aggiuntivo <code>istio</code>.</dd>
</dl>

#### `ibmcloud oc cluster-addon-enable kube-terminal`
{: #cs_cluster_addon_enable_kube-terminal}

Abilita il componente aggiuntivo [Kubernetes Terminal](/docs/containers?topic=containers-cs_cli_install#cli_web) per utilizzare questo terminale nella console del cluster {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable kube-terminal --cluster CLUSTER [--version VERSION]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Facoltativo: specifica la versione del componente aggiuntivo da installare. Se non viene specificata alcuna versione, viene installata quella predefinita.</dd>
</dl>
</br>

### `ibmcloud oc cluster-addons`
{: #cs_cluster_addons}

Elenca i componenti aggiuntivi gestiti che sono abilitati in un cluster.
{: shortdesc}



```
ibmcloud oc cluster-addons --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>
</dl>


</br>

### `ibmcloud oc cluster-config`
{: #cs_cluster_config}

Dopo aver eseguito l'accesso, scarica i dati di configurazione e i certificati di Kubernetes per connetterti al tuo cluster ed eseguire i comandi `oc`. I file vengono scaricati in `user_home_directory/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>`.
{: shortdesc}



```
ibmcloud oc cluster-config --cluster CLUSTER [--admin] [--export] [--network] [--powershell] [--skip-rbac] [-s] [--yaml]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo del servizio {{site.data.keyword.cloud_notm}} IAM **Visualizzatore** o **Lettore** per il cluster in {{site.data.keyword.containerlong_notm}}. Inoltre, se hai solo un ruolo della piattaforma o solo un ruolo del servizio, si applicano ulteriori restrizioni.
* **Piattaforma**: se hai solo un ruolo della piattaforma, puoi eseguire questo comando ma hai bisogno di un [ruolo del servizio](/docs/containers?topic=containers-users#platform) o di una [politica RBAC personalizzata](/docs/containers?topic=containers-users#role-binding) per eseguire azioni Kubernetes nel cluster.
* **Servizio**: se hai solo un ruolo del servizio, puoi eseguire questo comando. Tuttavia, il tuo amministratore cluster deve fornirti il nome e l'ID del cluster in quanto non puoi eseguire il comando `ibmcloud oc clusters` o avviare la console {{site.data.keyword.containerlong_notm}} per visualizzare i cluster. Dopo aver ricevuto il nome e l'ID del cluster, puoi [avviare il dashboard Kubernetes dalla CLI](/docs/containers?topic=containers-app#db_cli) e lavorare con Kubernetes.

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--admin</code></dt>
<dd>Scarica i certificati TLS e i file di autorizzazione per il ruolo Super utente. Puoi utilizzare i certificati per automatizzare le attività senza doverti riautenticare. I file vengono scaricati in `<user_home_directory>/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>-admin`. Questo valore è facoltativo.</dd>

<dt><code>--network</code></dt>
<dd>Scarica il file di configurazione Calico, i certificati TLS e i file di autorizzazione richiesti per eseguire i comandi <code>calicoctl</code> nel tuo cluster. Questo valore è facoltativo. **Nota**: per ottenere il comando di esportazione per i certificati e i dati di configurazione Kubernetes scaricati, devi eseguire il comando senza questo indicatore.</dd>

<dt><code>--export</code></dt>
<dd>Scarica i certificati e i dati di configurazione Kubernetes senza un messaggio diverso dal comando export. Poiché non viene visualizzato alcun messaggio, puoi utilizzare questo indicatore quando crei gli script automatizzati. Questo valore è facoltativo.</dd>

<dt><code>--powershell</code></dt>
<dd>Richiama le variabili di ambiente in formato Windows PowerShell.</dd>

<dt><code>--skip-rbac</code></dt>
<dd>Ignora l'aggiunta dei ruoli utente RBAC Kubernetes basati sui ruoli di accesso al servizio {{site.data.keyword.cloud_notm}} IAM alla configurazione del cluster. Includi questa opzione solo se [gestisci i tuoi propri ruoli RBAC Kubernetes](/docs/containers?topic=containers-users#rbac). Se utilizzi i [ruoli di accesso al servizio {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-access_reference#service) per gestire tutti i tuoi utenti RBAC, non includere questa opzione.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>

<dt><code>--yaml</code></dt>
<dd>Stampa l'output del comando in formato YAML. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-config --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc cluster-create`
{: #cs_cluster_create}

Crea un cluster nella tua organizzazione. Per i cluster gratuiti, specifica il nome del cluster; tutto il resto è impostato su un valore predefinito. Un cluster gratuito viene cancellato automaticamente dopo 30 giorni. Puoi avere un solo cluster gratuito alla volta. Per sfruttare tutte le funzionalità di Kubernetes, crea un cluster standard.
{: shortdesc}



```
ibmcloud oc cluster-create [--file FILE_LOCATION] [--hardware HARDWARE] --zone ZONE --machine-type MACHINE_TYPE --name NAME [--kube-version MAJOR.MINOR.PATCH] [--no-subnet] [--private-vlan PRIVATE_VLAN] [--public-vlan PUBLIC_VLAN] [--private-only] [--private-service-endpoint] [--public-service-endpoint] [--workers WORKER] [--disable-disk-encrypt] [-s]
```
{: pre}

**Autorizzazioni minime richieste**:
* Ruolo della piattaforma **Amministratore** per {{site.data.keyword.containerlong_notm}} a livello di account
* Ruolo della piattaforma **Amministratore** per {{site.data.keyword.registrylong_notm}} a livello di account
* Ruolo **Super utente** per l'infrastruttura IBM Cloud

**Opzioni comando**

<dl>
<dt><code>--file <em>FILE_LOCATION</em></code></dt>

<dd>Il percorso del file YAML per creare il tuo cluster standard. Invece di definire le caratteristiche del cluster utilizzando le opzioni fornite in questo comando, puoi utilizzare un file YAML. Questo valore è facoltativo per i cluster standard e non è disponibile per i cluster gratuiti. <p class="note">Se fornisci la stessa opzione nel comando come parametro nel file YAML, il valore nel comando ha la precedenza rispetto al valore nel YAML. Ad esempio, se definisci un'ubicazione nel tuo file YAML e utilizzi l'opzione <code>--zone</code> nel comando, il valore che hai immesso nell'opzione del comando sovrascrive il valore nel file YAML.</p>
<pre class="codeblock">
<code>name: <em>&lt;cluster_name&gt;</em>
zone: <em>&lt;zone&gt;</em>
no-subnet: <em>&lt;no-subnet&gt;</em>
machine-type: <em>&lt;machine_type&gt;</em>
private-vlan: <em>&lt;private_VLAN&gt;</em>
public-vlan: <em>&lt;public_VLAN&gt;</em>
private-service-endpoint: <em>&lt;true&gt;</em>
public-service-endpoint: <em>&lt;true&gt;</em>
hardware: <em>&lt;shared_or_dedicated&gt;</em>
workerNum: <em>&lt;number_workers&gt;</em>
kube-version: <em>&lt;kube-version&gt;</em>
diskEncryption: <em>false</em>
</code></pre>
</dd>

<dt><code>--hardware <em>HARDWARE</em></code></dt>
<dd>Il livello di isolamento hardware per il nodo di lavoro. Utilizza `dedicated` in modo che le risorse fisiche disponibili siano dedicate solo a te oppure `shared` per consentire la condivisione delle risorse fisiche con altri clienti IBM. L'impostazione predefinita è
`shared`. Questo valore è facoltativo per i cluster standard della VM e non è disponibile per i cluster gratuiti. Per i profili bare metal, specifica `dedicated`.</dd>

<dt><code>--zone <em>ZONE</em></code></dt>
<dd>La zona in cui vuoi creare il cluster. Questo valore è obbligatorio per i cluster standard. I cluster gratuiti possono essere creati nella regione che hai specificato con il comando <code>ibmcloud oc region-set</code>, ma non puoi specificare la zona.

<p>Controlla le [zone disponibili](/docs/containers?topic=containers-regions-and-zones#zones). Per estendere il tuo cluster tra le zone, devi crearlo in una [una zona che supporta il multizona](/docs/containers?topic=containers-regions-and-zones#zones).</p>

<p class="note">Quando selezioni una zona che si trova fuori dal tuo paese, tieni presente che potresti aver bisogno dell'autorizzazione legale prima che i dati possano essere archiviati fisicamente in un paese straniero.</p>
</dd>

<dt><code>--machine-type <em>MACHINE_TYPE</em></code></dt>
<dd>Scegli un profilo, o tipo di macchina, per i tuoi nodi di lavoro. Puoi distribuire i tuoi nodi di lavoro come macchine virtuali su hardware condiviso o dedicato o come macchine fisiche su bare metal. I profili fisici e virtuali disponibili variano in base alla zona in cui distribuisci il cluster. Per ulteriori informazioni, vedi la documentazione per il [comando](#cs_machine_types) `ibmcloud oc flavors (machine-types)`. Questo valore è obbligatorio per i cluster standard e non è disponibile per i cluster gratuiti.</dd>

<dt><code>--name <em>NAME</em></code></dt>
<dd>Il nome del cluster. Questo valore è obbligatorio. Il nome deve iniziare con una lettera, può contenere lettere, numeri e un trattino (-) e non può contenere più di 35 caratteri. Utilizza un nome che sia univoco tra le regioni. Il nome cluster e la regione in cui viene distribuito il cluster formano il nome dominio completo per il dominio secondario Ingress. Per garantire che il dominio secondario Ingress sia univoco all'interno di una regione, è possibile che il nome cluster venga troncato e vi venga aggiunto un valore casuale all'interno del nome dominio Ingress.
</dd>

<dt><code>--kube-version <em>MAJOR.MINOR.PATCH</em></code></dt>
<dd>La versione di Kubernetes per il nodo master del cluster. Questo valore è facoltativo. Quando la versione non viene specificata, il cluster viene creato con l'impostazione predefinita delle versioni di Kubernetes supportate. Per visualizzare le versioni disponibili, esegui <code>ibmcloud oc versions</code>.</dd>

<dt><code>--no-subnet</code></dt>
<dd>Per impostazione predefinita, vengono create una sottorete portatile pubblica e una privata sulla VLAN associata al cluster. Includi l'indicatore <code>--no-subnet</code> per evitare di creare sottoreti con il cluster. Puoi [creare](#cs_cluster_subnet_create) o [aggiungere](#cs_cluster_subnet_add) le sottoreti a un cluster in seguito.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>
<ul>
<li>Questo parametro non è disponibile per i cluster gratuiti.</li>
<li>Se si tratta del primo cluster standard che crei in questa zona, non includere questo indicatore. Una VLAN privata viene creata per te quando viene creato il cluster.</li>
<li>Se hai creato un cluster standard prima in questa zona o hai creato una VLAN privata nell'infrastruttura IBM prima, devi specificare tale VLAN privata. I router della VLAN privata iniziano sempre con <code>bcr</code> (router back-end) e i router della VLAN pubblica iniziano sempre con <code>fcr</code> (router front-end). Quando crei un cluster e specifichi le VLAN pubbliche e private, la combinazione di numeri e lettere dopo tali prefissi devono corrispondere.</li>
</ul>
<p>Per scoprire se già hai una VLAN privata per una specifica zona o per trovare il nome di una VLAN privata esistente, esegui <code>ibmcloud oc vlans --zone <em>&lt;zone&gt;</em></code>.</p></dd>

<dt><code>--public-vlan <em>PUBLIC_VLAN</em></code></dt>
<dd>
<ul>
<li>Questo parametro non è disponibile per i cluster gratuiti.</li>
<li>Se si tratta del primo cluster standard che crei in questa zona, non utilizzare questo indicatore. Alla creazione
del cluster, viene creata per te una VLAN pubblica.</li>
<li>Se hai creato prima un cluster standard in questa zona o hai creato una VLAN pubblica nell'infrastruttura IBM Cloud, specifica tale VLAN pubblica. Se vuoi collegare i tuoi nodi di lavoro solo a una VLAN privata, non specificare questa opzione. I router della VLAN privata iniziano sempre con <code>bcr</code> (router back-end) e i router della VLAN pubblica iniziano sempre con <code>fcr</code> (router front-end). Quando crei un cluster e specifichi le VLAN pubbliche e private, la combinazione di numeri e lettere dopo tali prefissi devono corrispondere.</li>
</ul>

<p>Per scoprire se già hai una VLAN pubblica per una specifica zona o per trovare il nome di una VLAN pubblica esistente, esegui <code>ibmcloud oc vlans --zone <em>&lt;zone&gt;</em></code>.</p></dd>

<dt><code>--private-only </code></dt>
<dd>Utilizza questa opzione per impedire la creazione di una VLAN pubblica. Obbligatoria solo quando specifichi l'indicatore `--private-vlan` e non includi l'indicatore `--public-vlan`.<p class="note">Se i nodi di lavoro sono configurati solo con una VLAN privata, devi abilitare l'endpoint del servizio privato o configurare un dispositivo gateway. Per ulteriori informazioni, vedi [Comunicazioni nodo di lavoro-master e utente-master](/docs/containers?topic=containers-plan_clusters#workeruser-master).</p></dd>

<dt><code>--private-service-endpoint</code></dt>
<dd>**Cluster standard che eseguono Kubernetes versione 1.11 o successiva in [account abilitati per VRF](/docs/resources?topic=resources-private-network-endpoints#getting-started)**: abilita l'[endpoint del servizio privato](/docs/containers?topic=containers-plan_clusters#workeruser-master) in modo che il tuo master Kubernetes e i nodi di lavoro comunichino sulla VLAN privata. Inoltre, puoi scegliere di abilitare l'endpoint del servizio pubblico utilizzando l'indicatore `--public-service-endpoint` per accedere al tuo cluster su Internet. Se abiliti solo l'endpoint del servizio privato, devi essere connesso alla VLAN privata per poter comunicare con il tuo master Kubernetes. Dopo aver abilitato un endpoint del servizio privato, non puoi disabilitarlo in seguito.<br><br>Dopo che hai creato il cluster, puoi ottenere l'endpoint eseguendo `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>`.</dd>

<dt><code>--public-service-endpoint</code></dt>
<dd>**Cluster standard che eseguono Kubernetes versione 1.11 o successiva**: abilita l'[endpoint del servizio pubblico](/docs/containers?topic=containers-plan_clusters#workeruser-master) in modo che il tuo master Kubernetes sia accessibile tramite la rete pubblica, ad esempio per eseguire i comandi `oc` dal tuo terminale. Se hai un [account abilitato a VRF](/docs/resources?topic=resources-private-network-endpoints#getting-started) e includi anche l'indicatore `--private-service-endpoint`, le comunicazioni tra master e nodi di lavoro passano sulla rete privata e su quella pubblica. Puoi disabilitare in seguito l'endpoint del servizio pubblico se vuoi un cluster solo privato.<br><br>Dopo che hai creato il cluster, puoi ottenere l'endpoint eseguendo `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>`.</dd>

<dt><code>--workers WORKER</code></dt>
<dd>Il numero di nodi di lavoro che vuoi distribuire nel tuo cluster. Se non specifici questa opzione, viene creato un cluster con un nodo di lavoro. Questo valore è facoltativo per i cluster standard e non è disponibile per i cluster gratuiti.
<p class="important">Se crei un cluster con solo un singolo nodo di lavoro per ogni zona, potresti riscontrare dei problemi con Ingress. Per l'alta disponibilità, crea un cluster con almeno due nodi di lavoro per ogni zona.</br>
</br>A ogni nodo di lavoro viene assegnato un ID e nome dominio univoco che non deve essere modificato manualmente dopo la creazione del cluster. La modifica dell'ID o del nome dominio impedisce al master Kubernetes di gestire il tuo cluster.</p></dd>

<dt><code>--disable-disk-encrypt</code></dt>
<dd>I nodi di lavoro sono dotati di crittografia disco AES a 256 bit per impostazione predefinita; [ulteriori informazioni](/docs/containers?topic=containers-security#encrypted_disk). Per disabilitare la crittografia, includi questa opzione.</dd>
</dl>



**<code>-s</code>**</br>
Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.

**Esempi**:


**Crea un cluster gratuito**: specifica solo il nome del cluster; tutto il resto è impostato su un valore predefinito. Un cluster gratuito viene cancellato automaticamente dopo 30 giorni. Puoi avere un solo cluster gratuito alla volta. Per sfruttare tutte le funzionalità di Kubernetes, crea un cluster standard.

```
ibmcloud oc cluster-create --name my_cluster
```
{: pre}

**Crea il tuo primo cluster standard**: il primo cluster standard che viene creato in una zona crea anche una VLAN privata. Pertanto, non includere l'indicatore `--public-vlan`.
{: #example_cluster_create}

```
ibmcloud oc cluster-create --zone dal10 --private-vlan my_private_VLAN_ID --machine-type b3c.4x16 --name my_cluster --hardware shared --workers 2
```
{: pre}

**Crea i successivi cluster standard**: se hai già creato un cluster standard in questa zona o hai creato una VLAN pubblica nell'infrastruttura IBM Cloud, specifica tale VLAN pubblica con l'indicatore `--public-vlan`. Per scoprire se già hai una VLAN pubblica per una specifica zona o trovare il nome di una VLAN pubblica esistente, esegui `ibmcloud oc vlans --zone <zone>`.

```
ibmcloud oc cluster-create --zone dal10 --public-vlan my_public_VLAN_ID --private-vlan my_private_VLAN_ID --machine-type b3c.4x16 --name my_cluster --hardware shared --workers 2
```
{: pre}

</br>

### `ibmcloud oc cluster-feature-disable public-service-endpoint`
{: #cs_cluster_feature_disable}

Disabilita l'endpoint del servizio pubblico per un cluster.
{: shortdesc}



**Importante**: prima di disabilitare l'endpoint pubblico, devi completare la seguente procedura per abilitare l'endpoint del servizio privato.
1. Abilita l'endpoint del servizio privato eseguendo `ibmcloud oc cluster-feature-enable private-service-endpoint --cluster <cluster_name>`.
2. Segui la richiesta nella CLI per aggiornare il server API del master Kubernetes.
3. [Ricarica tutti i nodi di lavoro nel tuo cluster per acquisire la configurazione dell'endpoint privato.](#cs_worker_reload)

```
ibmcloud oc cluster-feature-disable public-service-endpoint --cluster CLUSTER [-s] [-f]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-feature-disable public-service-endpoint --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc cluster-feature-enable`
{: #cs_cluster_feature_enable}

Abilita una funzione su un cluster esistente. Questo comando deve essere combinato con uno dei seguenti comandi secondari per la funzione che vuoi abilitare.
{: shortdesc}



#### `ibmcloud oc cluster-feature-enable private-service-endpoint`
{: #cs_cluster_feature_enable_private_service_endpoint}

Abilita l'[endpoint del servizio privato](/docs/containers?topic=containers-plan_clusters#workeruser-master) per rendere il tuo master cluster accessibile in modo privato.
{: shortdesc}

Per eseguire questo comando:
1. Abilita [VRF](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) nel tuo account dell'infrastruttura IBM Cloud. Per controllare se una VRF è già abilitata, utilizza il comando `ibmcloud account show`.
2. [Abilita il tuo account {{site.data.keyword.cloud_notm}} per l'utilizzo degli endpoint del servizio](/docs/resources?topic=resources-private-network-endpoints#getting-started).
3. Run `ibmcloud oc cluster-feature-enable private-service-endpoint --cluster <cluster_name>`.
4. Segui la richiesta nella CLI per aggiornare il server API del master Kubernetes.
5. [Ricarica tutti i nodi di lavoro](#cs_worker_reload) nel tuo cluster per acquisire la configurazione dell'endpoint privato.

```
ibmcloud oc cluster-feature-enable private-service-endpoint --cluster CLUSTER [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-feature-enable private-service-endpoint --cluster my_cluster
```
{: pre}

#### `ibmcloud oc cluster-feature-enable public-service-endpoint`
{: #cs_cluster_feature_enable_public_service_endpoint}

Abilita l'[endpoint del servizio pubblico](/docs/containers?topic=containers-plan_clusters#workeruser-master) per rendere il tuo master cluster accessibile pubblicamente.
{: shortdesc}

Dopo aver eseguito questo comando, devi aggiornare il server API per utilizzare l'endpoint del servizio seguendo il prompt nella CLI.

```
ibmcloud oc cluster-feature-enable public-service-endpoint --cluster CLUSTER [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-feature-enable public-service-endpoint --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc cluster-get`
{: #cs_cluster_get}

Visualizza i dettagli di un cluster.
{: shortdesc}



```
ibmcloud oc cluster-get --cluster CLUSTER [--json] [--showResources] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code><em>--showResources</em></code></dt>
<dd>Mostra più risorse del cluster come componenti aggiuntivi, VLAN, sottoreti e archiviazione.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-get --cluster my_cluster --showResources
```
{: pre}

**Output di esempio**:
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

Subnet VLANs
  VLAN ID   Subnet CIDR         Public   User-managed
  2234947   10.xxx.xx.xxx/29    false    false
  2234945   169.xx.xxx.xxx/29  true    false

```
{: screen}

</br>
### `ibmcloud oc cluster-pull-secret-apply`
{: #cs_cluster_pull_secret_apply}

Crea un ID del servizio {{site.data.keyword.cloud_notm}} IAM per il cluster, crea una politica per l'ID servizio che assegna il ruolo di accesso al servizio **Lettore** in {{site.data.keyword.registrylong_notm}}, quindi crea una chiave API per l'ID servizio. La chiave API viene quindi memorizzata in un `imagePullSecret` Kubernetes in modo che tu possa eseguire il pull di immagini dagli spazi dei nomi {{site.data.keyword.registryshort_notm}} per i contenitori che si trovano nello spazio dei nomi Kubernetes di `default`. Questo processo si verifica automaticamente quando crei un cluster. Se riscontri un errore durante il processo di creazione del cluster o hai un cluster esistente, puoi utilizzare questo comando per applicare nuovamente il processo.
{: shortdesc}

Questo metodo della chiave API sostituisce il precedente metodo di autorizzazione di un cluster ad accedere a {{site.data.keyword.registrylong_notm}} creando automaticamente un [token](/docs/services/Registry?topic=registry-registry_access#registry_tokens) e memorizzando tale token in un segreto di pull dell'immagine. Adesso, utilizzando le chiavi API IAM per accedere a {{site.data.keyword.registrylong_notm}}, puoi personalizzare le politiche IAM per l'ID servizio per limitare l'accesso ai tuoi spazi dei nomi o a immagini specifiche. Ad esempio, puoi modificare le politiche dell'ID servizio nel segreto di pull dell'immagine del cluster per eseguire il pull di immagini solo da una determinata regione o un determinato spazio dei nomi del registro. Prima di poter personalizzare le politiche IAM, devi [abilitare le politiche {{site.data.keyword.cloud_notm}} IAM per {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-user#existing_users).

Per ulteriori informazioni, vedi [Informazioni su come il tuo cluster è autorizzato e eseguire il pull di immagini da {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).



<p class="important">Quando esegui questo comando, viene avviata la creazione delle credenziali IAM e dei segreti di pull dell'immagine il cui completamento potrebbe richiedere alcuni minuti. Non puoi distribuire contenitori che estraggono un'immagine dai domini `icr.io` di {{site.data.keyword.registrylong_notm}} finché non vengono creati i segreti di pull dell'immagine. Per controllare i segreti di pull dell'immagine, esegui `oc get secrets | grep icr`.</br></br>Se hai aggiunto politiche IAM a un ID servizio esistente, come ad esempio per limitare l'accesso a un registro regionale, questo comando reimposta l'ID servizio, le politiche IAM e la chiave API per il segreto di pull dell'immagine.</p>

```
ibmcloud oc cluster-pull-secret-apply --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**:
*  Ruolo della piattaforma **Operatore o Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}
*  Ruolo della piattaforma **Amministratore** in {{site.data.keyword.registrylong_notm}}

**Opzioni comando**:

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>
</dl>

</br>

### `ibmcloud oc cluster-rm`
{: #cs_cluster_rm}

Rimuovere un cluster dalla tua organizzazione.
{: shortdesc}



```
ibmcloud oc cluster-rm --cluster CLUSTER [--force-delete-storage] [-f] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--force-delete-storage</code></dt>
<dd>Elimina il cluster e l'archiviazione persistente utilizzata dal cluster. **Attenzione**: se includi questo indicatore, non sarà possibile ripristinare i dati memorizzati nel cluster o le sue istanze di archiviazione associate. Questo valore è facoltativo.</dd>

<dt><code>-f</code></dt>
<dd>Utilizza questa opzione per forzare la rimozione di un cluster senza richiedere l'intervento dell'utente. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-rm --cluster my_cluster
```
{: pre}

</br>

### `ibmcloud oc cluster-update`
{: #cs_cluster_update}

Aggiorna il master Kubernetes alla versione API predefinita. Durante l'aggiornamento, non è possibile accedere o modificare il cluster. I nodi di lavoro, le applicazioni e le risorse che sono state distribuite dall'utente non vengono modificate e continuano a essere eseguite.
{: shortdesc}

Potresti dover modificare i tuoi file YAML per distribuzioni future. Controlla questa [nota sulla release](/docs/containers?topic=containers-cs_versions) per i dettagli.



```
ibmcloud oc cluster-update --cluster CLUSTER [--kube-version MAJOR.MINOR.PATCH] [--force-update] [-f] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--kube-version <em>MAJOR.MINOR.PATCH</em></code></dt>
<dd>La versione Kubernetes del cluster. Se non specifichi una versione, il master Kubernetes viene aggiornato alla versione API predefinita. Per visualizzare le versioni disponibili, esegui [ibmcloud oc kube-versions](#cs_kube_versions). Questo valore è facoltativo.</dd>

<dt><code>--force-update</code></dt>
<dd>Prova l'aggiornamento anche se la modifica è maggiore di due versioni secondarie rispetto alla versione del nodo di lavoro. Questo valore è facoltativo.</dd>

<dt><code>-f</code></dt>
<dd>Forza l'esecuzione del comando senza richiedere l'intervento dell'utente. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-update --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc clusters`
{: #cs_clusters}

Elenca tutti i cluster nel tuo account {{site.data.keyword.cloud_notm}}.
{: shortdesc}



Vengono restituiti i cluster in tutte le ubicazioni. Per filtrare i cluster in base a una specifica ubicazione, includi l'indicatore `--locations`. Ad esempio, se filtri i cluster per l'area metropolitana `dal`, vengono restituiti i cluster multizona e i cluster a zona singola nei data center (zone) all'interno di quell'area metropolitana. Se filtri i cluster per il data center (zona) `dal10`, vengono restituiti i cluster multizona che hanno un nodo di lavoro in quella zona e i cluster a zona singola in quella zona. Puoi passare un'ubicazione o un elenco di ubicazioni separate da virgole.

Se utilizzi la versione `0.2` beta (legacy) del plug-in {{site.data.keyword.containerlong_notm}}, vengono restituiti solo i cluster che si trovano nella regione a cui sei attualmente indirizzato. Per passare da una regione a un'altra, esegui `ibmcloud oc region-set`.
{: deprecated}

```
ibmcloud oc clusters [--locations LOCATION] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--locations <em>LOCATION</em></code></dt>
<dd>Filtra le zone in base a una specifica ubicazione o a un elenco di ubicazioni separate da virgole. Per visualizzare le ubicazioni supportate, esegui <code>ibmcloud oc supported-locations</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc clusters --locations ams03,wdc,ap
```
{: pre}

</br>
### Obsoleto: `ibmcloud oc kube-versions`
{: #cs_kube_versions}

Visualizza un elenco di versioni di Kubernetes supportate in {{site.data.keyword.containerlong_notm}}. Aggiorna i tuoi [master cluster](#cs_cluster_update) e [nodi di lavoro](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_update) alla versione predefinita per le funzionalità stabili più recenti.
{: shortdesc}

Questo comando è stato dichiarato obsoleto. Utilizza invece il [comando `ibmcloud oc versions`](#cs_versions_command).
{: deprecated}

```
ibmcloud oc kube-versions [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

**Opzioni comando**:
<dl>
<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc kube-versions
```
{: pre}

</br>

### `ibmcloud oc versions`
{: #cs_versions_command}

Elenca tutte le versioni della piattaforma del contenitore disponibili per i cluster {{site.data.keyword.containerlong_notm}}. Aggiorna i tuoi [master cluster](#cs_cluster_update) e [nodi di lavoro](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_update) alla versione predefinita per le funzionalità stabili più recenti.
{: shortdesc}



```
ibmcloud oc versions [--show-version PLATFORM][--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

**Opzioni comando**:
<dl>
<dt><code>--show-version</code> <em>PLATFORM</em></dt>
<dd>Mostra solo le versioni per la piattaforma del contenitore specificata. I valori supportati sono <code>kubernetes</code> o <code>openshift</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc versions
```
{: pre}

<br />



## Comandi cluster: servizi e integrazioni
{: #cluster_services_commands}

### `ibmcloud oc cluster-service-bind`
{: #cs_cluster_service_bind}

Crea le credenziali del servizio di un servizio {{site.data.keyword.cloud_notm}} e archivia queste credenziali in un segreto Kubernetes nel tuo cluster. Per visualizzare i servizi {{site.data.keyword.cloud_notm}} disponibili dal catalogo {{site.data.keyword.cloud_notm}}, esegui `ibmcloud service offerings`. **Nota**: puoi aggiungere solo servizi {{site.data.keyword.cloud_notm}} che supportano le chiavi del servizio.
{: shortdesc}

Per ulteriori informazioni sul bind del servizio e su quali servizi puoi aggiungere al tuo cluster, vedi [Aggiunta di servizi attraverso il bind del servizio IBM Cloud](/docs/containers?topic=containers-service-binding).



```
ibmcloud oc cluster-service-bind --cluster CLUSTER --namespace KUBERNETES_NAMESPACE --service SERVICE_INSTANCE [--key SERVICE_INSTANCE_KEY] [--role IAM_SERVICE_ROLE] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}} e ruolo Cloud Foundry **Sviluppatore**

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--key <em>SERVICE_INSTANCE_KEY</em></code></dt>
<dd>Il nome o il GUID di una chiave di servizio esistente. Questo valore è facoltativo. Quando utilizzi il comando `service-binding`, le nuove credenziali del servizio vengono create automaticamente per la tua istanza del servizio e viene assegnato il ruolo di accesso del servizio **Scrittore** IAM per i servizi abilitati a IAM. Se vuoi utilizzare una chiave del servizio esistente che hai creato in precedenza, utilizza questa opzione. Se definisci una chiave del servizio, non puoi impostare contemporaneamente l'opzione `--role` perché le tue chiavi del servizio sono già state create con uno specifico ruolo di accesso del servizio IAM. </dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>Il nome dello spazio dei nomi Kubernetes dove desideri creare il segreto Kubernetes per le tue credenziali del servizio. Questo valore è obbligatorio.</dd>

<dt><code>--service <em>SERVICE_INSTANCE</em></code></dt>
<dd>Il nome dell'istanza del servizio {{site.data.keyword.cloud_notm}} di cui vuoi eseguire il bind. Per trovare il nome, esegui <code>ibmcloud service list</code> per i servizi Cloud Foundry e <code>ibmcloud resource service-instances</code> per i servizi abilitati a IAM. Questo valore è obbligatorio. </dd>

<dt><code>--role <em>IAM_SERVICE_ROLE</em></code></dt>
<dd>Il ruolo {{site.data.keyword.cloud_notm}} IAM che vuoi per la chiave di servizio. Questo valore è facoltativo e può essere utilizzato solo per i servizi abilitati a IAM. Se non imposti questa opzione, le tue credenziali del servizio vengono create automaticamente e viene assegnato loro il ruolo del servizio di accesso **Scrittore** di IAM. Se vuoi utilizzare delle chiavi di servizio esistenti specificando l'opzione `--key`, non includere questa opzione.<br><br>
Per elencare i ruoli disponibili per il servizio, esegui `ibmcloud iam roles --service <service_name>`. Il nome servizio è il nome del servizio nel catalogo che puoi ottenere eseguendo `ibmcloud catalog search`.  </dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-service-bind --cluster my_cluster --namespace my_namespace --service my_service_instance
```
{: pre}

</br>
### `ibmcloud oc cluster-service-unbind`
{: #cs_cluster_service_unbind}

Rimuovi un servizio {{site.data.keyword.cloud_notm}} da un cluster annullandone il bind a uno spazio dei nomi Kubernetes.
{: shortdesc}



Quando rimuovi un servizio {{site.data.keyword.cloud_notm}}, le credenziali del servizio vengono rimosse dal cluster. Se un pod sta ancora utilizzando il servizio,
si verificherà un errore perché non è possibile trovare le credenziali del servizio.
{: tip}

```
ibmcloud oc cluster-service-unbind --cluster CLUSTER --namespace KUBERNETES_NAMESPACE --service SERVICE_INSTANCE [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}} e ruolo Cloud Foundry **Sviluppatore**

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>Il nome dello spazio di nomi Kubernetes. Questo valore è obbligatorio.</dd>

<dt><code>--service <em>SERVICE_INSTANCE</em></code></dt>
<dd>Il nome dell'istanza del servizio {{site.data.keyword.cloud_notm}} che vuoi rimuovere. Per trovare il nome dell'istanza del servizio, esegui `ibmcloud oc cluster-services --cluster <cluster_name_or_ID>`. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-service-unbind --cluster my_cluster --namespace my_namespace --service 8567221
```
{: pre}

</br>
### `ibmcloud oc cluster-services`
{: #cs_cluster_services}

Elencare i servizi associati a uno o a tutti gli spazi dei nomi Kubernetes in un cluster. Se non viene specificata
alcuna opzione, vengono visualizzati i servizi per lo spazio dei nomi predefinito.
{: shortdesc}



```
ibmcloud oc cluster-services --cluster CLUSTER [--namespace KUBERNETES_NAMESPACE] [--all-namespaces] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code>, <code>-n
<em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>Includi i servizi associati a uno specifico spazio dei nomi in un cluster. Questo valore è facoltativo.</dd>

<dt><code>--all-namespaces</code></dt>
<dd>Includi i servizi associati a tutti gli spazi dei nomi in un cluster. Questo valore è facoltativo.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-services --cluster my_cluster --namespace my_namespace
```
{: pre}

</br>
### `ibmcloud oc va`
{: #cs_va}

Una volta che hai [installato il programma di scansione del contenitore](/docs/services/va?topic=va-va_index#va_install_container_scanner), visualizza un report dettagliato della valutazione della vulnerabilità per un contenitore nel tuo cluster.
{: shortdesc}



```
ibmcloud oc va --container CONTAINER_ID [--extended] [--vulnerabilities] [--configuration-issues] [--json]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo di accesso al servizio **Lettore** per {{site.data.keyword.registrylong_notm}}. **Nota**: non assegnare le politiche per {{site.data.keyword.registryshort_notm}} al livello del gruppo di risorse.

**Opzioni comando**:
<dl>
<dt><code>--container CONTAINER_ID</code></dt>
<dd><p>L'ID del contenitore. Questo valore è obbligatorio.</p>
<p>Per trovare l'ID del tuo contenitore:<ol><li>[Indirizza la CLI Kubernetes al tuo cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).</li><li>Elenca i tuoi pod eseguendo `oc get pods`.</li><li>Trova il campo **Container ID** nell'output del comando `oc describe pod <pod_name>`. Ad esempio, `Container ID: containerd://1a11a1aa2b2b22223333c44444ccc555667d7dd777888e8ef99f1011121314g15`.</li><li>Rimuovi il prefisso `containerd://` dall'ID prima di utilizzare l'ID contenitore per il comando `ibmcloud oc va`. Ad esempio, `1a11a1aa2b2b22223333c44444ccc555667d7dd777888e8ef99f1011121314g15`.</li></ol></p></dd>

<dt><code>--extended</code></dt>
<dd><p>Estende l'output del comando per mostrare maggiori informazioni di correzione per i pacchetti vulnerabili. Questo valore è facoltativo.</p>
<p>Per impostazione predefinita, i risultati della scansione mostrano l'ID, lo stato della politica, i pacchetti interessati e come risolvere il problema. Con l'indicatore `--extended`, aggiunge le informazioni come il riepilogo, gli avvisi di sicurezza del fornitore e il link all'avviso ufficiale.</p></dd>

<dt><code>--vulnerabilities</code></dt>
<dd>Limita l'output del comando in modo da visualizzare solo le vulnerabilità del pacchetto. Questo valore è facoltativo. Non puoi utilizzare questo indicatore se usi l'indicatore `--configuration-issues`.</dd>

<dt><code>--configuration-issues</code></dt>
<dd>Limita l'output del comando in modo da visualizzare solo i problemi di configurazione. Questo valore è facoltativo. Non puoi utilizzare questo indicatore se usi l'indicatore `--vulnerabilities` flag.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc va --container 1a11a1aa2b2b22223333c44444ccc555667d7dd777888e8ef99f1011121314g15 --extended --vulnerabilities --json
```
{: pre}

</br>
### Beta: `ibmcloud oc key-protect-enable`
{: #cs_key_protect}

Crittografa i segreti Kubernetes utilizzando [{{site.data.keyword.keymanagementservicefull}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/key-protect?topic=key-protect-getting-started-tutorial#getting-started-tutorial) come [provider KMS (key management service) ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) nel tuo cluster. Per ruotare una chiave in un cluster con crittografia chiave esistente, riesegui questo comando con un nuovo ID chiave root.
{: shortdesc}

Non eliminare le chiavi root nella tua istanza {{site.data.keyword.keymanagementserviceshort}}. Non eliminare le chiavi anche se le ruoti per utilizzare una nuova chiave. Se elimini una chiave root non puoi accedere ai dati in etcd o ai dati dei segreti presenti nel tuo cluster o rimuoverli.
{: important}



```
ibmcloud oc key-protect-enable --cluster CLUSTER_NAME_OR_ID --key-protect-url ENDPOINT --key-protect-instance INSTANCE_GUID --crk ROOT_KEY_ID
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--container CLUSTER_NAME_OR_ID</code></dt>
<dd>Il nome o l'ID del cluster.</dd>

<dt><code>--key-protect-url ENDPOINT</code></dt>
<dd>L'endpoint {{site.data.keyword.keymanagementserviceshort}} per l'istanza del cluster. Per ottenere l'endpoint, vedi [endpoint del servizio per regione](/docs/services/key-protect?topic=key-protect-regions#service-endpoints).</dd>

<dt><code>--key-protect-instance INSTANCE_GUID</code></dt>
<dd>Il GUID della tua istanza {{site.data.keyword.keymanagementserviceshort}}. Per ottenere il GUID dell'istanza, esegui <code>ibmcloud resource service-instance SERVICE_INSTANCE_NAME --id</code> e copia il secondo valore (non l'intero CRN).</dd>

<dt><code>--crk ROOT_KEY_ID</code></dt>
<dd>L'ID della chiave root {{site.data.keyword.keymanagementserviceshort}}. Per ottenere la CRK, vedi [Visualizzazione delle chiavi](/docs/services/key-protect?topic=key-protect-view-keys#view-keys).</dd>
</dl>

**Esempio**:
```
ibmcloud oc key-protect-enable --cluster mycluster --key-protect-url keyprotect.us-south.bluemix.net --key-protect-instance a11aa11a-bbb2-3333-d444-e5e555e5ee5 --crk 1a111a1a-bb22-3c3c-4d44-55e555e55e55
```
{: pre}

</br>
### `ibmcloud oc webhook-create`
{: #cs_webhook_create}

Registra un webhook.
{: shortdesc}



```
ibmcloud oc webhook-create --cluster CLUSTER --level LEVEL --type slack --url URL  [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--level <em>LEVEL</em></code></dt>
<dd>Il livello di notifica, come ad esempio <code>Normal</code> o
<code>Warning</code>. <code>Warning</code> è il valore predefinito. Questo valore è facoltativo.</dd>

<dt><code>--type <em>slack</em></code></dt>
<dd>Il tipo di webhook. Attualmente, Slack è supportato. Questo valore è obbligatorio.</dd>

<dt><code>--url <em>URL</em></code></dt>
<dd>L'URL del webhook. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc webhook-create --cluster my_cluster --level Normal --type slack --url http://github.com/mywebhook
```
{: pre}

<br />


## Comandi cluster: sottoreti
{: #cluster_subnets_commands}



### `ibmcloud oc cluster-subnet-add`
{: #cs_cluster_subnet_add}

Rendi una sottorete privata o pubblica portatile esistente nel tuo account dell'infrastruttura IBM Cloud disponibile a un cluster oppure riutilizza le sottoreti da un cluster eliminato invece di utilizzare le sottoreti di cui è stato eseguito il provisioning automaticamente.
{: shortdesc}



<p class="important">Gli indirizzi IP pubblici portatili vengono addebitati mensilmente. Se rimuovi gli indirizzi IP pubblici portatili dopo aver eseguito il provisioning del tuo cluster, devi comunque pagare l'addebito mensile anche se li hai utilizzati solo per un breve periodo di tempo.</br>
</br>Quando rendi disponibile una sottorete a un cluster, gli indirizzi IP di questa sottorete vengono utilizzati per scopi di rete del cluster. Per evitare conflitti di indirizzi IP, assicurati di utilizzare una sottorete con un solo cluster. Non utilizzare una sottorete per più cluster o per altri
scopi al di fuori di {{site.data.keyword.containerlong_notm}} contemporaneamente.</br>
</br>Per consentire le comunicazioni tra i nodi di lavoro che si trovano in diverse sottoreti sulla stessa VLAN in account non VRF, devi [abilitare l'instradamento tra le sottoreti sulla stessa VLAN](/docs/containers?topic=containers-subnets#subnet-routing).</p>

```
ibmcloud oc cluster-subnet-add --cluster CLUSTER --subnet-id SUBNET [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--subnet-id <em>SUBNET</em></code></dt>
<dd>L'ID della sottorete. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-subnet-add --cluster my_cluster --subnet-id 1643389
```
{: pre}

</br>

### `ibmcloud oc cluster-subnet-create`
{: #cs_cluster_subnet_create}

Crea una sottorete portatile in un account dell'infrastruttura IBM Cloud sulla tua VLAN pubblica o privata e rendila disponibile a un cluster.
{: shortdesc}



<p class="important">Quando rendi disponibile una sottorete a un cluster, gli indirizzi IP di questa sottorete vengono utilizzati per scopi di rete del cluster. Per evitare conflitti di indirizzi IP, assicurati di utilizzare una sottorete con un solo cluster. Non utilizzare una sottorete per più cluster o per altri
scopi al di fuori di {{site.data.keyword.containerlong_notm}} contemporaneamente.</br>
</br>Se hai più VLAN per un cluster, più sottoreti sulla stessa VLAN o un cluster multizona, devi abilitare una [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) per il tuo account dell'infrastruttura IBM Cloud in modo che i tuoi nodi di lavoro possano comunicare tra loro sulla rete privata. Per abilitare VRF, [contatta il tuo rappresentante dell'account dell'infrastruttura IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Per controllare se una VRF è già abilitata, utilizza il comando `ibmcloud account show`. Se non puoi o non vuoi abilitare VRF, abilita lo [spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Per eseguire questa azione, ti serve l'[autorizzazione dell'infrastruttura](/docs/containers?topic=containers-users#infra_access) **Rete > Gestisci il VLAN Spanning di rete** oppure puoi richiedere al proprietario dell'account di abilitarlo. Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando `ibmcloud oc vlan-spanning-get --region <region>`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get).</p>

```
ibmcloud oc cluster-subnet-create --cluster CLUSTER --size SIZE --vlan VLAN_ID [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio. Per elencare i tuoi cluster, utilizza il [comando](#cs_clusters) `ibmcloud oc clusters`.</dd>

<dt><code>--size <em>SIZE</em></code></dt>
<dd>Il numero di indirizzi IP che desideri creare nella sottorete portatile. I valori accettati sono 8, 16, 32 o 64. <p class="note"> Quando aggiungi gli indirizzi IP portatili per la tua sottorete, tre indirizzi IP vengono utilizzati per stabilire un collegamento di rete interno al cluster. Non puoi utilizzare questi tre indirizzi IP per i tuoi ALB (application load balancer) Ingress o per creare servizi NLB (network load balancer). Ad esempio, se richiedi otto indirizzi IP pubblici portatili, puoi utilizzarne cinque per esporre le tue applicazioni pubblicamente.</p> </dd>

<dt><code>--vlan <em>VLAN_ID</em></code></dt>
<dd>L'ID della VLAN pubblica o privata su cui desideri creare la sottorete. Devi selezionare una VLAN pubblica o privata a cui è connesso un nodo di lavoro esistente. Per riesaminare le VLAN pubbliche o private a cui sono connessi i tuoi nodi di lavoro, esegui <code>ibmcloud oc cluster-get --cluster &lt;cluster&gt; --showResources</code> e cerca la sezione <strong>Subnet VLANs</strong> nell'output. Il provisioning della sottorete viene eseguito nella stessa zona in cui si trova la VLAN.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-subnet-create --cluster my_cluster --size 8 --vlan 1764905
```
{: pre}

</br>

### `ibmcloud oc cluster-subnet-detach`
{: #cs_cluster_subnet_detach}

Scollega una sottorete portatile pubblica o privata in un account dell'infrastruttura IBM Cloud da un cluster. La sottorete rimane disponibile nel tuo account dell'infrastruttura IBM Cloud. **Nota**: ogni servizio distribuito a un indirizzo IP dalla sottorete rimane attivo dopo la rimozione della sottorete.
{: shortdesc}

<p class="note"><img src="images/icon-classic.png" alt="Icona del provider dell'infrastruttura classica" width="15" style="width:15px; border-style: none"/> Comando solo classico.</p>

```
ibmcloud oc cluster-subnet-detach --cluster CLUSTER --subent-id SUBNET_ID [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio. Per elencare i tuoi cluster, utilizza il [comando](#cs_clusters) `ibmcloud oc clusters`.</dd>

<dt><code>--vlan <em>VLAN_ID</em></code></dt>
<dd>L'ID della sottorete pubblica o privata che vuoi scollegare. Per trovare l'ID della sottorete, esegui prima <code>ibmcloud oc cluster-get --cluster &lt;cluster&gt; --showResources</code> e cerca il CIDR della sottorete nella sezione <strong>Subnet VLANs</strong> dell'output. Quindi, utilizzando il CIDR della sottorete, esegui <code>ibmcloud oc subnets</code> e cerca l'<strong>ID</strong> della sottorete.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-subnet-detach --cluster my_cluster --subnet-id 1602829
```
{: pre}

</br>

### `ibmcloud oc cluster-user-subnet-add`
{: #cs_cluster_user_subnet_add}

Porta la tua sottorete privata nei cluster {{site.data.keyword.containerlong_notm}}.
{: shortdesc}



Questa sottorete privata non è una fornita dall'infrastruttura IBM Cloud. In quanto tale, devi configurare l'instradamento del traffico di rete in entrata e in uscita per la sottorete. Per aggiungere una sottorete dell'infrastruttura IBM Cloud, utilizza il [comando](#cs_cluster_subnet_add) `ibmcloud oc cluster-subnet-add`.

<p class="important">Quando rendi disponibile una sottorete a un cluster, gli indirizzi IP di questa sottorete vengono utilizzati per scopi di rete del cluster. Per evitare conflitti di indirizzi IP, assicurati di utilizzare una sottorete con un solo cluster. Non utilizzare una sottorete per più cluster o per altri
scopi al di fuori di {{site.data.keyword.containerlong_notm}} contemporaneamente.</br>
</br>Se hai più VLAN per un cluster, più sottoreti sulla stessa VLAN o un cluster multizona, devi abilitare una [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) per il tuo account dell'infrastruttura IBM Cloud in modo che i tuoi nodi di lavoro possano comunicare tra loro sulla rete privata. Per abilitare VRF, [contatta il tuo rappresentante dell'account dell'infrastruttura IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Per controllare se una VRF è già abilitata, utilizza il comando `ibmcloud account show`. Se non puoi o non vuoi abilitare VRF, abilita lo [spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Per eseguire questa azione, ti serve l'[autorizzazione dell'infrastruttura](/docs/containers?topic=containers-users#infra_access) **Rete > Gestisci il VLAN Spanning di rete** oppure puoi richiedere al proprietario dell'account di abilitarlo. Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando `ibmcloud oc vlan-spanning-get --region <region>`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get).</p>

```
ibmcloud oc cluster-user-subnet-add --cluster CLUSTER --subnet-cidr SUBNET_CIDR --private-vlan PRIVATE_VLAN
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--subnet-cidr <em>SUBNET_CIDR</em></code></dt>
<dd>La sottorete CIDR (Classless InterDomain Routing). Questo valore è obbligatorio e non deve essere in conflitto con le sottoreti utilizzate dall'infrastruttura IBM Cloud. L'intervallo di prefissi supportati è compreso tra `/30` (1 indirizzo IP) e `/24` (253 indirizzi IP). Se configuri il CIDR con una lunghezza di prefisso e successivamente devi modificarla, aggiungi prima il nuovo CIDR e quindi [rimuovi il vecchio CIDR](#cs_cluster_user_subnet_rm).</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>L'ID della VLAN privata. Questo valore è obbligatorio. L'ID deve essere per una VLAN privata nel cluster in cui si trovano uno o più nodi di lavoro. Per visualizzare le VLAN private nel tuo cluster, esegui `ibmcloud oc cluster-get --cluster <cluster_name_or_ID> --showResources`. Nella sezione **Subnet VLANs** dell'output, cerca le VLAN che hanno un valore **Public** di `false`.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-user-subnet-add --cluster my_cluster --subnet-cidr 169.xx.xxx.xxx/29 --private-vlan 1502175
```
{: pre}

</br>
### `ibmcloud oc cluster-user-subnet-rm`
{: #cs_cluster_user_subnet_rm}

Rimuovi la tua sottorete privata da un cluster specificato. Ogni servizio distribuito con un indirizzo IP dalla tua sottorete privata rimane attivo dopo la rimozione della sottorete.
{: shortdesc}



```
ibmcloud oc cluster-user-subnet-rm --cluster CLUSTER --subnet-cidr SUBNET_CIDR --private-vlan PRIVATE_VLAN
```
{: pre}
**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--subnet-cidr <em>SUBNET_CIDR</em></code></dt>
<dd>La sottorete CIDR (Classless InterDomain Routing). Questo valore è obbligatorio e deve corrispondere al CIDR configurato dal [commando](#cs_cluster_user_subnet_add) `ibmcloud oc cluster-user-subnet-add`.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>L'ID della VLAN privata. Questo valore è obbligatorio e deve corrispondere all'ID della VLAN configurato dal [comando](#cs_cluster_user_subnet_add) `ibmcloud oc cluster-user-subnet-add`.</dd>
</dl>

**Esempio**:
```
ibmcloud oc cluster-user-subnet-rm --cluster my_cluster --subnet-cidr 169.xx.xxx.xxx/29 --private-vlan 1502175
```
{: pre}

</br>
### `ibmcloud oc subnets`
{: #cs_subnets}

Elenca le sottoreti portatili disponibili nel tuo account dell'infrastruttura IBM Cloud..
{: shortdesc}



```
ibmcloud oc subnets [--locations LOCATIONS] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>

<dt><code>--locations <em>LOCATION</em></code></dt>
<dd>Filtra le zone in base a una specifica ubicazione o a un elenco di ubicazioni separate da virgole. Per visualizzare le ubicazioni supportate, esegui <code>ibmcloud oc supported-locations</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc subnets --locations ams03,wdc,ap
```
{: pre}

<br />


## Comandi ALB (application load balancer) Ingress
{: #alb_commands}

### `ibmcloud oc alb-autoupdate-disable`
{: #cs_alb_autoupdate_disable}

Disabilita gli aggiornamenti automatici di tutti i pod Ingress ALB in un cluster.
{: shortdesc}



Per impostazione predefinita, gli aggiornamenti automatici per il componente aggiuntivo ALB (application load balancer) Ingress sono abilitati. I pod ALB vengono aggiornati automaticamente quando è disponibile una nuova versione di build. Per aggiornare invece il componente aggiuntivo manualmente, utilizza questo comando per disabilitare gli aggiornamenti automatici. Puoi quindi aggiornare i pod ALB eseguendo il [comando `ibmcloud oc alb-update`](#cs_alb_update).

Quando aggiorni la versione Kubernetes principale o secondaria del tuo cluster, IBM apporta automaticamente le modifiche necessarie alla distribuzione di Ingress, ma non modifica la versione di build del tuo componente aggiuntivo ALB Ingress. Sei responsabile della verifica della compatibilità delle ultime versioni di Kubernetes e delle immagini del componente aggiuntivo ALB Ingress.

```
ibmcloud oc alb-autoupdate-disable --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Esempio**:
```
ibmcloud oc alb-autoupdate-disable --cluster mycluster
```
{: pre}

</br>
### `ibmcloud oc alb-autoupdate-enable`
{: #cs_alb_autoupdate_enable}

Abilita gli aggiornamenti automatici di tutti i pod Ingress ALB in un cluster.
{: shortdesc}

Se gli aggiornamenti automatici per il componente aggiuntivo ALB Ingress sono disabilitati, puoi riabilitarli. Ogni volta che diventa disponibile la versione di build successiva, gli ALB vengono aggiornati automaticamente all'ultima build.



```
ibmcloud oc alb-autoupdate-enable --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

</br>
### `ibmcloud oc alb-autoupdate-get`
{: #cs_alb_autoupdate_get}

Controlla se gli aggiornamenti automatici per il componente aggiuntivo ALB Ingress sono abilitati e se i tuoi ALB sono aggiornati all'ultima versione di build.
{: shortdesc}



```
ibmcloud oc alb-autoupdate-get --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

</br>
### Beta: `ibmcloud oc alb-cert-deploy`
{: #cs_alb_cert_deploy}

Distribuisci o aggiorna un certificato dalla tua istanza {{site.data.keyword.cloudcerts_long_notm}} all'ALB in un cluster.
{: shortdesc}



Quando importi un certificato con questo comando, il segreto del certificato viene creato in uno spazio dei nomi chiamato `ibm-cert-store`. Un riferimento a questo segreto viene quindi creato nello spazio dei nomi `default`, a cui può accedere qualsiasi risorsa Ingress in qualsiasi spazio dei nomi. Quando l'ALB elabora le richieste, segue questo riferimento per raccogliere e utilizzare il segreto del certificato dallo spazio dei nomi `ibm-cert-store`.

Puoi anche utilizzare il parametro `--update` per aggiornare i certificati, ad esempio per aggiornare il certificato nel tuo cluster dopo che hai rinnovato il certificato in {{site.data.keyword.cloudcerts_short}}. Puoi soltanto aggiornare i certificati importati dalla stessa istanza {{site.data.keyword.cloudcerts_long_notm}}.

Per rimanere entro i [limiti di velocità](https://cloud.ibm.com/apidocs/certificate-manager#rate-limiting) impostati da {{site.data.keyword.cloudcerts_short}}, attendi almeno 45 secondi tra i successivi comandi `alb-cert-deploy` e `alb-cert-deploy --update`.
{: note}

```
ibmcloud oc alb-cert-deploy [--update] --cluster CLUSTER --secret-name SECRET_NAME --cert-crn CERTIFICATE_CRN [--update] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--update</code></dt>
<dd>Aggiorna il certificato per un segreto dell'ALB in un cluster. Puoi utilizzare questo parametro per aggiornare il certificato dopo che lo hai rinnovato in {{site.data.keyword.cloudcerts_short}}.</dd>

<dt><code>--secret-name <em>SECRET_NAME</em></code></dt>
<dd>Specifica un nome per il segreto ALB quando viene creato nel cluster. Questo valore è obbligatorio. Assicurati di non creare il segreto con lo stesso nome del segreto Ingress fornito da IBM. Puoi ottenere il nome del segreto Ingress fornito da IBM eseguendo <code>ibmcloud oc cluster-get --cluster <cluster_name_or_ID> | grep Ingress</code>.</dd>

<dt><code>--cert-crn <em>CERTIFICATE_CRN</em></code></dt>
<dd>Il CRN del certificato. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempi**:

Esempio per distribuire un segreto dell'ALB:
```
ibmcloud oc alb-cert-deploy --secret-name my_alb_secret --cluster my_cluster --cert-crn crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:4bc35b7e0badb304e60aef00947ae7ff
```
{: pre}

Esempio per aggiornare un segreto dell'ALB esistente:
```
ibmcloud oc alb-cert-deploy --update --secret-name my_alb_secret --cluster my_cluster --cert-crn crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:7e21fde8ee84a96d29240327daee3eb2
```
{: pre}

</br>
### Beta: `ibmcloud oc alb-cert-get`
{: #cs_alb_cert_get}

Se hai importato un certificato da {{site.data.keyword.cloudcerts_short}} all'ALB in un cluster, visualizza le informazioni sul certificato TLS, come i segreti a cui è associato.
{: shortdesc}



```
ibmcloud oc alb-cert-get --cluster CLUSTER [--secret-name SECRET_NAME] [--cert-crn CERTIFICATE_CRN] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--secret-name <em>SECRET_NAME</em></code></dt>
<dd>Il nome del segreto ALB. Questo valore è obbligatorio per ottenere le informazioni su un segreto specifico dell'ALB nel cluster.</dd>

<dt><code>--cert-crn <em>CERTIFICATE_CRN</em></code></dt>
<dd>Il CRN del certificato. Questo valore è obbligatorio per ottenere le informazioni su tutti i segreti dell'ALB che corrispondono a un CRN del certificato specifico nel cluster.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempi**:

Esempio per ottenere informazioni su un segreto ALB:
```
ibmcloud oc alb-cert-get --cluster my_cluster --secret-name my_alb_secret
```
{: pre}

Esempio per ottenere informazioni su tutti i segreti ALB che corrispondono a uno specifico certificato CRN:
```
ibmcloud oc alb-cert-get --cluster my_cluster --cert-crn  crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:4bc35b7e0badb304e60aef00947ae7ff
```
{: pre}

</br>
### Beta: `ibmcloud oc alb-cert-rm`
{: #cs_alb_cert_rm}

Se hai importato un certificato da {{site.data.keyword.cloudcerts_short}} all'ALB in un cluster, rimuovi il segreto dal cluster.
{: shortdesc}



Per rimanere entro i [limiti di velocità](https://cloud.ibm.com/apidocs/certificate-manager#rate-limiting) impostati da {{site.data.keyword.cloudcerts_short}}, attendi almeno 45 secondi tra i successivi comandi `alb-cert-rm`.
{: note}

```
ibmcloud oc alb-cert-rm --cluster CLUSTER [--secret-name SECRET_NAME] [--cert-crn CERTIFICATE_CRN] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--secret-name <em>SECRET_NAME</em></code></dt>
<dd>Il nome del segreto ALB. Questo valore è obbligatorio per rimuovere un segreto specifico dell'ALB nel cluster.</dd>

<dt><code>--cert-crn <em>CERTIFICATE_CRN</em></code></dt>
<dd>Il CRN del certificato. Questo valore è obbligatorio per rimuovere tutti i segreti dell'ALB che corrispondono a un CRN del certificato specifico nel cluster.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>

</dl>

**Esempi**:

Esempio per rimuovere un segreto dell'ALB:
```
ibmcloud oc alb-cert-rm --cluster my_cluster --secret-name my_alb_secret
```
{: pre}

Esempio per rimuovere tutti i segreti dell'ALB che corrispondono a un CRN del certificato specificato:
```
ibmcloud oc alb-cert-rm --cluster my_cluster --cert-crn crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:4bc35b7e0badb304e60aef00947ae7ff
```
{: pre}

</br>
### `ibmcloud oc alb-certs`
{: #cs_alb_certs}

Elenca i certificati che hai importato dalla tua istanza {{site.data.keyword.cloudcerts_long_notm}} agli ALB in un cluster.
{: shortdesc}



```
ibmcloud oc alb-certs --cluster CLUSTER [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc alb-certs --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc alb-configure`
{: #cs_alb_configure}

Abilita o disabilita un ALB nel tuo cluster standard.
{: shortdesc}

Puoi utilizzare questo comando per:
* Abilitare un ALB privato predefinito. Quando crei un cluster, viene creato un ALB privato predefinito per tuo conto in ciascuna zona in cui hai dei nodi di lavoro e una sottorete privata disponibile ma gli ALB privati predefiniti non sono abilitati. Tuttavia, tutti gli ALB pubblici predefiniti sono abilitati automaticamente.
* Abilitare un ALB che era stato precedentemente disabilitato.
* Disabilitare un ALB.
* Disabilitare la distribuzione ALB fornita da IBM in modo da poter distribuire il tuo controller Ingress e avvalerti della registrazione DNS per il dominio secondario Ingress fornito da IBM o il servizio del programma di bilanciamento del carico utilizzato per esporre il controller Ingress.

```
ibmcloud oc alb-configure --albID ALB_ID --disable|--enable [--user-ip USER_IP]|--disable-deployment [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--albID <em>ALB_ID</em></code></dt>
<dd>L'ID per un ALB. Per visualizzare gli ID per gli ALB in un cluster, esegui <code>ibmcloud oc albs --cluster <em>CLUSTER</em></code>. Questo valore è obbligatorio.</dd>

<dt><code>--disable</code></dt>
<dd>Includi questo indicatore per disabilitare un ALB in un cluster. <p class="note">Se disabiliti un ALB, l'indirizzo IP utilizzato dall'ALB torna nel pool degli IP portatili disponibili in modo che un altro servizio possa utilizzare l'IP. Se successivamente provi a riabilitare l'ALB, l'ALB potrebbe notificare un errore se l'indirizzo IP che utilizzava in precedenza è ora utilizzato da un altro servizio. Puoi arrestare l'esecuzione dell'altro servizio oppure specificare un altro indirizzo IP da utilizzare quando riabiliti l'ALB.</p></dd>

<dt><code>--enable</code></dt>
<dd>Includi questo indicatore per abilitare un ALB in un cluster.</dd>

<dt><code>--user-ip <em>USER_IP</em></code></dt>
<dd>Facoltativo: se abiliti l'ALB con l'indicatore <code>--enable</code>, puoi specificare un indirizzo IP che si trova su una VLAN nella zona in cui è stato creato l'ALB. L'ALB viene abilitato con, e utilizza, questo indirizzo IP pubblico o privato. <strong>Nota</strong>: questo indirizzo IP non deve essere utilizzato da un altro programma di bilanciamento del carico o ALB nel cluster. Se non viene fornito alcun indirizzo IP, l'ALB viene distribuito con un indirizzo IP pubblico o privato dalla sottorete pubblica o privata portatile di cui era stato eseguito automaticamente il provisioning quando hai creato il cluster oppure l'indirizzo IP pubblico o privato che hai precedentemente assegnato all'ALB.</dd>

<dt><code>--disable-deployment</code></dt>
<dd>Includi questo indicatore per disabilitare la distribuzione ALB fornita da IBM. Questo indicatore non rimuove la registrazione DNS per il dominio secondario Ingress fornito da IBM o per il servizio del programma di bilanciamento del carico utilizzato per esporre il controller Ingress.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempi**:

Esempio per abilitare un ALB:
```
ibmcloud oc alb-configure --albID private-cr18a61a63a6a94b658596aa93a087aaa9-alb1 --enable
```
{: pre}

Esempio per abilitare un ALB con un indirizzo IP fornito dall'utente:
```
ibmcloud oc alb-configure --albID private-cr18a61a63a6a94b658596aa93a087aaa9-alb1 --enable --user-ip user_ip
```
{: pre}

Esempio per disabilitare un ALB:
```
ibmcloud oc alb-configure --albID public-cr18a61a63a6a94b658596aa93a087aaa9-alb1 --disable
```
{: pre}

</br>

### `ibmcloud oc alb-get`
{: #cs_alb_get}

Visualizza i dettagli di un Ingress ALB in un cluster.
{: shortdesc}



```
ibmcloud oc alb-get --albID ALB_ID [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--albID <em>ALB_ID</em></code></dt>
<dd>L'ID per un ALB. Per visualizzare gli ID per gli ALB in un cluster, esegui <code>ibmcloud oc albs --cluster <em>CLUSTER</em></code>. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc alb-get --albID public-cr18a61a63a6a94b658596aa93a087aaa9-alb1
```
{: pre}

</br>
### `ibmcloud oc alb-rollback`
{: #cs_alb_rollback}

Se i tuoi pod ALB sono stati aggiornati di recente, ma una configurazione personalizzata per gli ALB è interessata dall'ultima build, puoi eseguire il rollback dell'aggiornamento alla build in cui i tuoi pod ALB erano precedentemente in esecuzione. Tutti i pod ALB nel cluster vengono ripristinati al loro stato di esecuzione precedente.
{: shortdesc}

Dopo aver eseguito il rollback di un aggiornamento, gli aggiornamenti automatici per i pod ALB sono disabilitati. Per riabilitare gli aggiornamenti automatici, utilizza il [comando `alb-autoupdate-enable`](#cs_alb_autoupdate_enable).



```
ibmcloud oc alb-rollback --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

</br>
### `ibmcloud oc alb-types`
{: #cs_alb_types}

Elenca i tipi ALB Ingress supportati.
{: shortdesc}



```
ibmcloud oc alb-types [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

</br>

### `ibmcloud oc alb-update`
{: #cs_alb_update}

Forza un aggiornamento dei pod Ingress ALB nel cluster alla versione più recente.
{: shortdesc}



Se gli aggiornamenti automatici per il componente aggiuntivo ALB Ingress sono disabilitati e vuoi aggiornare il componente aggiuntivo, puoi forzare un aggiornamento una tantum per i tuoi pod ALB. Quando scegli di aggiornare manualmente il componente aggiuntivo, tutti i pod ALB nel cluster vengono aggiornati all'ultima build. Non puoi aggiornare un singolo ALB o scegliere a quale build aggiornare il componente aggiuntivo. Gli aggiornamenti automatici rimangono disabilitati.

Quando aggiorni la versione Kubernetes principale o secondaria del tuo cluster, IBM apporta automaticamente le modifiche necessarie alla distribuzione di Ingress, ma non modifica la versione di build del tuo componente aggiuntivo ALB Ingress. Sei responsabile della verifica della compatibilità delle ultime versioni di Kubernetes e delle immagini del componente aggiuntivo ALB Ingress.

```
ibmcloud oc alb-update --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

</br>
### `ibmcloud oc albs`
{: #cs_albs}

Elenca tutti gli ID ALB Ingress in un cluster e visualizza se è disponibile un aggiornamento per i pod ALB.
{: shortdesc}



Se non viene restituito alcun ID ALB, il cluster non ha una sottorete portatile. Puoi [creare](#cs_cluster_subnet_create) o [aggiungere](#cs_cluster_subnet_add) le sottoreti a un cluster.
{: tip}

```
ibmcloud oc albs --cluster CLUSTER [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code><em>--cluster </em>CLUSTER</code></dt>
<dd>Il nome o l'ID del cluster in cui elenchi gli ALB disponibili. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc albs --cluster my_cluster
```
{: pre}

<br />



## Comandi infrastruttura
{: #infrastructure_commands}

### `ibmcloud oc api-key-info`
{: #cs_api_key_info}

Visualizza il nome e l'indirizzo e-mail per il proprietario della chiave API {{site.data.keyword.cloud_notm}} IAM (Identity and Access Management) in un gruppo di risorse {{site.data.keyword.containerlong_notm}}.
{: shortdesc}



La chiave API {{site.data.keyword.cloud_notm}} viene impostata automaticamente per un gruppo di risorse e una regione quando viene eseguita la prima azione che richiede la politica di accesso come amministratore {{site.data.keyword.containerlong_notm}}. Ad esempio, uno dei tuoi utenti amministratore crea il primo cluster nel gruppo di risorse `default` della regione `us-south`. In questo modo, la chiave API {{site.data.keyword.cloud_notm}} IAM di questo utente viene memorizzata nell'account per tale gruppo di risorse e regione. La chiave API viene utilizzata per ordinare le risorse nell'infrastruttura IBM Cloud, come nuovi nodi di lavoro o VLAN. È possibile impostare una chiave API differente per ogni regione all'interno di un gruppo di risorse.

Quando un altro utente esegue un'azione in questo gruppo di risorse e in questa regione che richiede l'interazione con il portfolio dell'infrastruttura IBM Cloud, come la creazione di un nuovo cluster o il ricaricamento di un nodo di lavoro, la chiave API memorizzata viene utilizzata per determinare se esistono autorizzazioni sufficienti per eseguire tale azione. Per garantire che le azioni correlate all'infrastruttura nel tuo cluster possano essere eseguite correttamente, assegna ai tuoi utenti amministratore {{site.data.keyword.containerlong_notm}} la politica di accesso all'infrastruttura **Super utente**. Per ulteriori informazioni, vedi [Gestione dell'accesso utente](/docs/containers?topic=containers-users#infra_access).

Se ritieni di dover aggiornare la chiave API memorizzata per un gruppo di risorse e una regione, puoi farlo eseguendo il comando [ibmcloud oc api-key-reset](#cs_api_key_reset). Questo comando richiede la politica di accesso come amministratore {{site.data.keyword.containerlong_notm}} e memorizza la chiave API dell'utente che esegue questo comando nell'account.

**Suggerimento:** la chiave API restituita in questo comando potrebbe non essere utilizzata se le credenziali dell'infrastruttura IBM Cloud sono state impostate manualmente utilizzando il comando [ibmcloud oc credential-set](#cs_credentials_set).

```
ibmcloud oc api-key-info --cluster CLUSTER [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>

</dl>

**Esempio**:
```
ibmcloud oc api-key-info --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc api-key-reset`
{: #cs_api_key_reset}

sostituisci la chiave API IAM {{site.data.keyword.cloud_notm}} corrente in un gruppo di risorse {{site.data.keyword.cloud_notm}} e una regione {{site.data.keyword.containershort_notm}}.
{: shortdesc}



Questo comando richiede la politica di accesso come amministratore {{site.data.keyword.containerlong_notm}} e memorizza la chiave API dell'utente che esegue questo comando nell'account. La chiave API {{site.data.keyword.cloud_notm}} IAM è necessaria per ordinare l'infrastruttura dal portfolio dell'infrastruttura IBM Cloud. Una volta memorizzata, la chiave API viene utilizzata per ogni azione in una regione che richiede autorizzazioni di infrastruttura indipendenti dall'utente che esegue questo comando. Per ulteriori informazioni su come funzionano le chiavi API {{site.data.keyword.cloud_notm}} IAM, vedi il [comando `ibmcloud oc api-key-info`](#cs_api_key_info).

Prima di utilizzare questo comando, assicurati che l'utente che lo esegue abbia le [autorizzazioni di {{site.data.keyword.containerlong_notm}} e dell'infrastruttura IBM Cloud necessarie](/docs/containers?topic=containers-users#users). Indica come destinazione il gruppo di risorse e la regione per cui vuoi impostare la chiave API.
{: important}

```
ibmcloud oc api-key-reset --region REGION [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Specifica una regione. Per elencare le regioni disponibili, esegui <code>ibmcloud oc regions</code>.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc api-key-reset --region us-south
```
{: pre}


</br>

### `ibmcloud oc credential-get`
{: #cs_credential_get}

Se configuri il tuo account {{site.data.keyword.cloud_notm}} per utilizzare credenziali differenti per accedere al portfolio dell'infrastruttura IBM Cloud, ottieni il nome utente dell'infrastruttura per la regione e il gruppo di risorse a cui sei attualmente indirizzato.
{: shortdesc}



```
ibmcloud oc credential-get --region REGION [-s] [--json]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Specifica una regione. Per elencare le regioni disponibili, esegui <code>ibmcloud oc regions</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc credential-get --region us-south
```
{: pre}

</br>
### `ibmcloud oc credential-set` (`credentials-set`)
{: #cs_credentials_set}

Imposta le credenziali per un gruppo di risorse e una regione in modo da poter accedere al portfolio dell'infrastruttura IBM Cloud tramite il tuo account {{site.data.keyword.cloud_notm}}.
{: shortdesc}



Se hai un account Pagamento a consumo {{site.data.keyword.cloud_notm}}, hai accesso al portfolio dell'infrastruttura IBM Cloud per impostazione predefinita. Tuttavia, potresti voler utilizzare un altro account dell'infrastruttura IBM Cloud di cui già disponi per ordinare l'infrastruttura. Puoi collegare l'account dell'infrastruttura al tuo account {{site.data.keyword.cloud_notm}} utilizzando questo comando.

Se le credenziali dell'infrastruttura IBM Cloud vengono impostate manualmente per una regione e un gruppo di risorse, queste credenziali vengono utilizzate per ordinare l'infrastruttura per tutti i cluster all'interno di tale regione nel gruppo di risorse. Queste credenziali vengono utilizzate per determinare le autorizzazioni di infrastruttura, anche se esiste una [{{site.data.keyword.cloud_notm}}chiave API IAM](#cs_api_key_info) per il gruppo di risorse e la regione. Se l'utente di cui sono state memorizzate le credenziali non dispone delle autorizzazioni necessarie per ordinare l'infrastruttura, le azioni relative all'infrastruttura, come la creazione di un cluster o il ricaricamento di un nodo di lavoro, possono avere esito negativo.

Non puoi impostare più credenziali per lo stesso gruppo di risorse e la stessa regione {{site.data.keyword.containerlong_notm}}.

Prima di utilizzare questo comando, assicurati che l'utente di cui vengono utilizzate le credenziali abbia le [autorizzazioni di {{site.data.keyword.containerlong_notm}} e dell'infrastruttura IBM Cloud necessarie](/docs/containers?topic=containers-users#users).
{: important}

```
ibmcloud oc credential-set --infrastructure-api-key API_KEY --infrastructure-username USERNAME --region REGION [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--infrastructure-username <em>USERNAME</em></code></dt>
<dd>Nome utente API dell'account dell'infrastruttura IBM Cloud. Questo valore è obbligatorio. Il nome utente API dell'infrastruttura non è uguale all'ID IBM. Per visualizzare il nome utente dell'API dell'infrastruttura, vedi [Gestione delle chiavi API dell'infrastruttura classica](/docs/iam?topic=iam-classic_keys).</dd>

<dt><code>--infrastructure-api-key <em>API_KEY</em></code></dt>
<dd>Chiave API dell'account dell'infrastruttura IBM Cloud. Questo valore è obbligatorio. Per visualizzare o generare una chiave API dell'infrastruttura, vedi [Gestione delle chiavi API dell'infrastruttura classica](/docs/iam?topic=iam-classic_keys).</dd>

<dt><code>--region <em>REGION</em></code></dt>
<dd>Specifica una regione. Per elencare le regioni disponibili, esegui <code>ibmcloud oc regions</code>.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc credential-set --infrastructure-api-key <api_key> --infrastructure-username dbmanager --region us-south
```
{: pre}

</br>
### `ibmcloud oc credential-unset`
{: #cs_credentials_unset}

Rimuovi le credenziali per un gruppo di risorse e una regione per rimuovere l'accesso al portfolio dell'infrastruttura IBM Cloud tramite il tuo account {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Dopo aver rimosso le credenziali, la [{{site.data.keyword.cloud_notm}}chiave API IAM](#cs_api_key_info) viene utilizzata per ordinare le risorse nell'infrastruttura IBM Cloud.



```
ibmcloud oc credential-unset --region REGION [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Specifica una regione. Per elencare le regioni disponibili, esegui <code>ibmcloud oc regions</code>.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc credential-unset --region us-south
```
{: pre}

</br>

### `ibmcloud oc flavors` (`machine-types`)
{: #cs_machine_types}

Visualizza un elenco di profili di nodo di lavoro disponibili. I profili variano in base alla zona.
{:shortdesc}



Ogni profilo include la quantità di CPU virtuale, memoria e spazio su disco per ogni nodo di lavoro nel cluster. Per impostazione predefinita, la directory del disco di archiviazione secondario, in cui vengono memorizzati tutti i dati del contenitore, è codificata con la crittografia LUKS. Se l'opzione `disable-disk-encrypt` viene inclusa durante la creazione del cluster, i dati di runtime del contenitore dell'host non vengono crittografati. [Ulteriori informazioni sulla crittografia](/docs/containers?topic=containers-security#encrypted_disk).

Puoi eseguire il provisioning del tuo nodo di lavoro come una macchina virtuale su hardware condiviso o dedicato o, solo per i cluster classici, come una macchina fisica su bare metal. [Ulteriori informazioni sulle tue opzioni di profilo](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes).

```
ibmcloud oc flavors --zone ZONE [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

**Opzioni comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Immetti la zona dove vuoi elencare i profili disponibili. Questo valore è obbligatorio. Per visualizzare le zone disponibili per i cluster classici, esegui `ibmcloud oc zones`.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc flavors --zone dal10
```
{: pre}


</br>

### `ibmcloud oc infra-permissions-get`
{: #infra_permissions_get}

Controlla se alle credenziali che consentono [l'accesso al portfolio dell'infrastruttura IBM Cloud](/docs/containers?topic=containers-users#api_key) per la regione e il gruppo di risorse indicati come destinazione mancano le autorizzazioni dell'infrastruttura consigliate o richieste.
{: shortdesc}



**Cosa significano le autorizzazioni dell'infrastruttura obbligatorie (`required`) e consigliate (`suggested`)?**<br>
Se alle credenziali dell'infrastruttura per la regione e il gruppo di risorse manca qualche autorizzazione, l'output di questo comando restituisce un elenco di autorizzazioni obbligatorie (`required`) e consigliate (`suggested`).
*   **Obbligatorie**: queste autorizzazioni sono necessarie per ordinare e gestire correttamente le risorse dell'infrastruttura quali i nodi di lavoro. Se alle credenziali dell'infrastruttura manca una di queste autorizzazioni, azioni comuni quali `worker-reload` possono non riuscire per tutti i cluster nella regione e nel gruppo di risorse.
*   **Consigliate**: queste autorizzazioni sono utili da includere nelle tue autorizzazioni dell'infrastruttura e, in alcuni casi d'uso, potrebbero essere necessarie. Ad esempio, l'autorizzazione dell'infrastruttura `Add Compute with Public Network Port` è consigliata perché, se vuoi una rete pubblica, hai bisogno di questa autorizzazione. Tuttavia, se il tuo caso d'uso è un cluster solo sulla VLAN privata, l'autorizzazione non è necessaria e quindi non è considerata obbligatoria (`required`).

Per un elenco dei casi d'uso comuni in base all'autorizzazione, vedi [Ruoli dell'infrastruttura](/docs/containers?topic=containers-access_reference#infra).

**Cosa succede se vedo un'autorizzazione dell'infrastruttura che non riesco a trovare nella console o nella tabella [Ruoli dell'infrastruttura](/docs/containers?topic=containers-access_reference#infra) ?**<br>
Le autorizzazioni `Support Case` sono gestite in una parte differente della console rispetto alle autorizzazioni dell'infrastruttura. Vedi il passo 8 di [Personalizzazione delle autorizzazioni di infrastruttura](/docs/containers?topic=containers-users#infra_access).

**Quali autorizzazioni dell'infrastruttura assegno?**<br>
Se le politiche della tua azienda in materia di autorizzazioni sono rigide, potresti dover limitare le autorizzazioni consigliate (`suggested`) per il caso d'uso del tuo cluster. Altrimenti, assicurati che le tue credenziali dell'infrastruttura per la regione e il gruppo di risorse includano tutte le autorizzazioni obbligatorie (`required`) e consigliate (`suggested`).

Per la maggior parte dei casi d'uso, [configura la chiave API](/docs/containers?topic=containers-users#api_key) per la regione e il gruppo di risorse con le autorizzazioni dell'infrastruttura appropriate. Se devi utilizzare un altro account dell'infrastruttura diverso dal tuo account corrente, [configura le credenziali manuali](/docs/containers?topic=containers-users#credentials).

**Come controllo quali azioni possono eseguire gli utenti?**<br>
Una volta configurate le credenziali dell'infrastruttura, puoi controllare quali azioni possono eseguire i tuoi utenti assegnando loro i [ruoli della piattaforma IAM {{site.data.keyword.cloud_notm}}Bluemix_notm>](/docs/containers?topic=containers-access_reference#iam_platform).

```
ibmcloud oc infra-permissions-get --region REGION [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Specifica una regione. Per elencare le regioni disponibili, esegui <code>ibmcloud oc regions</code>.Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc infra-permissions-get --region us-south
```
{: pre}

Output di esempio:
```
Missing Virtual Worker Permissions

Add Server                    suggested
Cancel Server                 suggested
View Virtual Server Details   required

Missing Physical Worker Permissions

No changes are suggested or required.

Missing Network Permissions

No changes are suggested or required.

Missing Storage Permissions

Add Storage       required
Manage Storage    required
```
{: screen}


</br>

### `ibmcloud oc vlan-spanning-get`
{: #cs_vlan_spanning_get}

Visualizza lo stato dello spanning della VLAN per un account dell'infrastruttura IBM Cloud. Lo spanning della VLAN abilita tutti i dispositivi su un account a comunicare tra loro tramite la rete privata, indipendentemente dalla loro VLAN assegnata.
{: shortdesc}

<p class="note">l'opzione di spanning della VLAN è disabilitata per i cluster creati in un account abilitato alla VRF. Quando la VRF è abilitata, tutte le VLAN nell'account possono automaticamente comunicare tra loro sulla rete privata. Per controllare se una VRF è abilitata, utilizza il comando `ibmcloud account show`. Per ulteriori informazioni, vedi [Pianificazione della configurazione di rete del tuo cluster: comunicazioni tra i nodi di lavoro](/docs/containers?topic=containers-plan_clusters#worker-worker).</p>

```
ibmcloud oc vlan-spanning-get --region REGION [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Specifica una regione. Per elencare le regioni disponibili, esegui <code>ibmcloud oc regions</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc vlan-spanning-get --region us-south
```
{: pre}

</br>
### `ibmcloud oc vlans`
{: #cs_vlans}

Elenca le VLAN pubbliche e private disponibili per una zona nel tuo account dell'infrastruttura IBM Cloud. Per elencare le VLAN disponibili,
devi avere un account a pagamento.
{: shortdesc}



```
ibmcloud oc vlans --zone ZONE [--all] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**:
* Per visualizzare le VLAN a cui è connesso il cluster in una zona: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}
* Per elencare tutte le VLAN disponibili in una zona: ruolo della piattaforma **Visualizzatore** per la regione in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Immetti la zona in cui vuoi elencare le tue VLAN pubbliche e private. Questo valore è obbligatorio. Per visualizzare le zone disponibili, esegui `ibmcloud oc zones`.</dd>

<dt><code>--all</code></dt>
<dd>Elenca tutte le VLAN disponibili. Per impostazione predefinita, le VLAN vengono filtrate per mostrare solo le VLAN valide. Perché sia valida, una VLAN deve essere associata a un'infrastruttura in grado di ospitare un nodo di lavoro con archiviazione su disco locale.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc vlans --zone dal10
```
{: pre}

</br>


<br />


## Comandi registrazione
{: #logging_commands}

### `ibmcloud oc apiserver-config-get audit-webhook`
{: #cs_apiserver_config_get}

Visualizza l'URL del servizio di registrazione remoto a cui stai inviando i log di controllo del server API. L'URL è stato specificato quando hai creato il back-end webhook per la configurazione del server API.
{: shortdesc}



```
ibmcloud oc apiserver-config-get audit-webhook --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>
</dl>

</br>

### `ibmcloud oc apiserver-config-set audit-webhook`
{: #cs_apiserver_config_set}

Imposta il back-end webhook per la configurazione del server API. Il back-end webhook inoltra i log di controllo del server API a un server remoto. Una configurazione webhook viene creata in base alle informazioni che fornisci negli indicatori di questo comando. Se non fornisci alcuna informazione negli indicatori, viene utilizzata una configurazione webhook predefinita. Dopo aver impostato il webhook, devi eseguire il comando `ibmcloud oc apiserver-refresh` per applicare le modifiche al master Kubernetes.
{: shortdesc}



```
ibmcloud oc apiserver-config-set audit-webhook --cluster CLUSTER [--remoteServer SERVER_URL_OR_IP] [--caCert CA_CERT_PATH] [--clientCert CLIENT_CERT_PATH] [--clientKey CLIENT_KEY_PATH]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--remoteServer <em>SERVER_URL</em></code></dt>
<dd>L'URL o l'indirizzo IP del servizio di registrazione remoto a cui vuoi inviare i log di controllo. Se fornisci un URL del server non sicuro, vengono ignorati tutti i certificati. Questo valore è facoltativo.</dd>

<dt><code>--caCert <em>CA_CERT_PATH</em></code></dt>
<dd>Il percorso del file per il certificato CA utilizzato per verificare il servizio di registrazione remoto. Questo valore è facoltativo.</dd>

<dt><code>--clientCert <em>CLIENT_CERT_PATH</em></code></dt>
<dd>Il percorso del file per il certificato client utilizzato per l'autenticazione con il servizio di registrazione remoto. Questo valore è facoltativo.</dd>

<dt><code>--clientKey <em> CLIENT_KEY_PATH</em></code></dt>
<dd>Il percorso del file per la chiave client corrispondente utilizzata per il collegamento al servizio di registrazione remoto. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc apiserver-config-set audit-webhook --cluster my_cluster --remoteServer https://audit.example.com/audit --caCert /mnt/etc/kubernetes/apiserver audit/ca.pem --clientCert /mnt/etc/kubernetes/apiserver audit/cert.pem --clientKey /mnt/etc/kubernetes/apiserver audit/key.pem
```
{: pre}

</br>
### `ibmcloud oc apiserver-config-unset audit-webhook`
{: #cs_apiserver_config_unset}

Disabilita la configurazione back-end webhook per il server API del cluster. La disabilitazione del back-end webhook interrompe l'inoltro dei log di controllo del server API a un server remoto.
{: shortdesc}



```
ibmcloud oc apiserver-config-unset audit-webhook --cluster CLUSTER
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>
</dl>

</br>

### `ibmcloud oc logging-autoupdate-disable`
{: #cs_log_autoupdate_disable}

Disabilita gli aggiornamenti automatici di tutti i pod Fluentd in un cluster.
{: shortdesc}



Disabilita gli aggiornamenti automatici dei tuoi pod Fluentd in un cluster specifico. Quando aggiorni la versione Kubernetes principale o secondaria del tuo cluster, IBM apporta automaticamente le modifiche necessarie alla mappa di configurazione Fluentd, ma non modifica la versione di build del tuo componente aggiuntivo Fluentd per la registrazione. Sei responsabile della verifica della compatibilità delle ultime versioni di Kubernetes e delle immagini del componente aggiuntivo.

```
ibmcloud oc logging-autoupdate-disable --cluster CLUSTER
```
{: pre}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster in cui vuoi disabilitare gli aggiornamenti automatici per il componente aggiuntivo Fluentd. Questo valore è obbligatorio.</dd>
</dl>

</br>

### `ibmcloud oc logging-autoupdate-enable`
{: #cs_log_autoupdate_enable}

Abilita gli aggiornamenti automatici per tuoi pod Fluentd in un cluster specifico. I pod Fluentd vengono aggiornati automaticamente quando è disponibile una nuova versione di build.
{: shortdesc}



```
ibmcloud oc logging-autoupdate-enable --cluster CLUSTER
```
{: pre}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster in cui vuoi abilitare gli aggiornamenti automatici per il componente aggiuntivo Fluentd. Questo valore è obbligatorio.</dd>
</dl>

</br>

### `ibmcloud oc logging-autoupdate-get`
{: #cs_log_autoupdate_get}

Visualizza se i pod Fluentd sono impostati per eseguire automaticamente l'aggiornamento in un cluster.
{: shortdesc}



```
ibmcloud oc logging-autoupdate-get --cluster CLUSTER
```
{: pre}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster in cui vuoi verificare se sono abilitati gli aggiornamenti automatici per il componente aggiuntivo Fluentd. Questo valore è obbligatorio.</dd>
</dl>

</br>

### `ibmcloud oc logging-collect`
{: #cs_log_collect}

Effettua una richiesta per un'istantanea dei tuoi log in un momento specifico e quindi memorizza i log in un bucket {{site.data.keyword.cos_full_notm}}.
{: shortdesc}



```
ibmcloud oc logging-collect --cluster CLUSTER --cos-bucket BUCKET_NAME --cos-endpoint ENDPOINT --hmac-key-id HMAC_KEY_ID --hmac-key HMAC_KEY --type LOG_TYPE [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster per cui vuoi creare un'istantanea.</dd>

<dt><code>--cos-bucket <em>BUCKET_NAME</em></code></dt>
<dd>Il nome del bucket {{site.data.keyword.cos_short}} in cui vuoi memorizzare i tuoi log.</dd>

<dt><code>--cos-endpoint <em>ENDPOINT</em></code></dt>
<dd>L'endpoint {{site.data.keyword.cos_short}} regionale, interregionale o a livello di singolo data center per il bucket in cui archivi i tuoi log. Per gli endpoint disponibili, vedi [Endpoint e ubicazioni di archiviazione](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints) nella documentazione di {{site.data.keyword.cos_short}}.</dd>

<dt><code>--hmac-key-id <em>HMAC_KEY_ID</em></code></dt>
<dd>L'ID univoco per le credenziali HMAC della tua istanza {{site.data.keyword.cos_short}}.</dd>

<dt><code>--hmac-key <em>HMAC_KEY</em></code></dt>
<dd>La chiave HMAC per la tua istanza {{site.data.keyword.cos_short}}.</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>Facoltativo; il tipo di log di cui vuoi creare un'istantanea. Attualmente, `master` è l'unica opzione, oltre a quella predefinita.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Comando di esempio**:

```
ibmcloud oc logging-collect --cluster mycluster --cos-bucket mybucket --cos-endpoint s3-api.us-geo.objectstorage.softlayer.net --hmac-key-id e2e7f5c9fo0144563c418dlhi3545m86 --hmac-key c485b9b9fo4376722f692b63743e65e1705301ab051em96j
```
{: pre}

**Output di esempio**:

```
There is no specified log type. The default master will be used.
Submitting log collection request for master logs for cluster mycluster...
  OK
  The log collection request was successfully submitted. To view the status of the request run ibmcloud oc logging-collect-status mycluster.
```
{: screen}

</br>
### `ibmcloud oc logging-collect-status`
{: #cs_log_collect_status}

Controlla lo stato della richiesta di istantanea della raccolta log per il tuo cluster.
{: shortdesc}



```
ibmcloud oc logging-collect-status --cluster CLUSTER [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Amministratore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster per cui vuoi creare un'istantanea. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Comando di esempio**:

```
ibmcloud oc logging-collect-status --cluster mycluster
```
{: pre}

**Output di esempio**:

```
Getting the status of the last log collection request for cluster mycluster...
  OK
  State     Start Time             Error   Log URLs
  success   2018-09-18 16:49 PDT   - s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-0-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
  s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-1-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
  s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-2-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
```
{: screen}

</br>
### `ibmcloud oc logging-config-create`
{: #cs_logging_create}

Crea una configurazione di registrazione. Puoi utilizzare questo comando per inoltrare i log dei contenitori, delle applicazioni, dei nodi di lavoro, dei cluster Kubernetes e dei programmi di bilanciamento del carico dell'applicazione Ingress a {{site.data.keyword.loganalysisshort_notm}} o a un server syslog esterno.
{: shortdesc}



```
ibmcloud oc logging-config-create --cluster CLUSTER --logsource LOG_SOURCE --type LOG_TYPE [--namespace KUBERNETES_NAMESPACE] [--hostname LOG_SERVER_HOSTNAME_OR_IP] [--port LOG_SERVER_PORT] [--space CLUSTER_SPACE] [--org CLUSTER_ORG] [--app-containers CONTAINERS] [--app-paths PATHS_TO_LOGS] [--syslog-protocol PROTOCOL]  [--json] [--skip-validation] [--force-update][-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster per tutte le origini log tranne `kube-audit` e ruolo della piattaforma **Amministratore** per il cluster per l'origine log `kube-audit`

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster.</dd>

<dt><code>--logsource <em>LOG_SOURCE</em></code></dt>
<dd>L'origine del log per abilitare l'inoltro di log. Questo argomento supporta un elenco separato da virgole di origini log da applicare per la configurazione. I valori accettati sono <code>container</code>, <code>application</code>, <code>worker</code>, <code>kubernetes</code>, <code>storage</code>, <code>ingress</code> e <code>kube-audit</code>. Se non fornisci un'origine log, vengono create le configurazioni per <code>container</code> e <code>ingress</code>.</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>Il luogo in cui vuoi inoltrare i tuoi log. Le opzioni sono <code>ibm</code>, che inoltra i tuoi log a {{site.data.keyword.loganalysisshort_notm}} e <code>syslog</code>, che inoltra i log a un server esterno.<p class="deprecated">{{site.data.keyword.loganalysisshort_notm}} è obsoleto. Questa opzione di comando è supportata fino al 30 settembre 2019.</p></dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>Lo spazio dei nomi Kubernetes dal quale desideri inoltrare i log. L'inoltro del log non è supportato per gli spazi dei nomi Kubernetes <code>ibm-system</code> e <code>kube-system</code>. Questo valore è valido solo per l'origine del log del contenitore ed è facoltativo. Se non specifichi uno spazio dei nomi, tutti gli spazi dei nomi nel cluster utilizzeranno questa configurazione.</dd>

<dt><code>--hostname <em>LOG_SERVER_HOSTNAME</em></code></dt>
<dd>Quando il tipo di registrazione è <code>syslog</code>, questo valore è il nome host o l'indirizzo IP del server di raccolta log. Questo valore è obbligatorio per <code>syslog</code>. Quando il tipo di registrazione è <code>ibm</code>, questo valore è l'URL di inserimento {{site.data.keyword.loganalysislong_notm}}. Puoi trovare l'elenco degli URL di inserimento disponibili [qui](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_ingestion#log_ingestion_urls). Se non specifichi un URL di inserimento, viene utilizzato l'endpoint della regione in cui è stato creato il tuo cluster.</dd>

<dt><code>--port <em>LOG_SERVER_PORT</em></code></dt>
<dd>La porta del server di raccolta del log. Questo valore è facoltativo. Se non specifichi una porta, viene utilizzata la porta standard <code>514</code> per <code>syslog</code> e <code>9091</code> per <code>ibm</code>.</dd>

<dt><code>--space <em>CLUSTER_SPACE</em></code></dt>
<dd>Facoltativo: il nome dello spazio Cloud Foundry a cui vuoi inviare i log. Questo valore è valido solo per il tipo di log <code>ibm</code> ed è facoltativo. Se non specifichi uno spazio, i log vengono inviati al livello dell'account. Se lo specifichi, devi specificare anche un'<code>org</code>.</dd>

<dt><code>--org <em>CLUSTER_ORG</em></code></dt>
<dd>Facoltativo: il nome dell'organizzazione Cloud Foundry in cui si trova lo spazio. Questo valore è valido solo per il tipo di log <code>ibm</code> ed è obbligatorio se hai specificato uno spazio.</dd>

<dt><code>--app-paths</code></dt>
<dd>Il percorso sul contenitore a cui si collegano le applicazioni. Per inoltrare i log con il tipo di origine <code>application</code>, devi fornire un percorso. Per specificare più di un percorso, utilizza un elenco separato da virgole. Questo valore è necessario per l'origine log <code>application</code>. Esempio: <code>/var/log/myApp1/&ast;,/var/log/myApp2/&ast;</code></dd>

<dt><code>--syslog-protocol</code></dt>
<dd>Il protocollo del livello di trasferimento utilizzato quando il tipo di registrazione è <code>syslog</code>. I valori supportati sono <code>tcp</code>, <code>tls</code> e il valore predefinito <code>udp</code>. Quando esegui l'inoltro a un server rsyslog con il protocollo <code>udp</code>, i log superiori a 1KB vengono troncati.</dd>

<dt><code>--app-containers</code></dt>
<dd>Per inoltrare i log dalle applicazioni, puoi specificare il nome del contenitore che contiene la tua applicazione. Puoi specificare più di un contenitore utilizzando un elenco separato da virgole. Se non si specificano i contenitori, i log vengono inoltrati da tutti i contenitori che contengono i percorsi da te forniti. Questa opzione è valida solo per l'origine log <code>application</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>--skip-validation</code></dt>
<dd>Ignora la convalida dei nomi di organizzazione e spazio quando vengono specificati. La mancata convalida riduce il tempo di elaborazione, ma una configurazione di registrazione non valida non inoltra correttamente i log. Questo valore è facoltativo.</dd>

<dt><code>--force-update</code></dt>
<dd>Forza i tuoi pod Fluentd ad eseguire l'aggiornamento alla versione più recente. La versione di Fluentd deve essere la più recente per modificare le tue configurazioni di registrazione.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempi**:

Esempio del tipo di log `syslog` che inoltra da un'origine log `container` sulla porta predefinita 514:
```
ibmcloud oc logging-config-create my_cluster --logsource container --namespace my_namespace  --hostname 169.xx.xxx.xxx --type syslog
```
{: pre}

Esempio di un tipo di log `syslog` che inoltra i log da un'origine `ingress` su una porta differente dalla predefinita:
```
ibmcloud oc logging-config-create --cluster my_cluster --logsource container --hostname 169.xx.xxx.xxx --port 5514 --type syslog
```
{: pre}

</br>
### `ibmcloud oc logging-config-get`
{: #cs_logging_get}

Visualizza tutte le configurazioni di inoltro log per un cluster o filtra le configurazioni di registrazione in base all'origine del log.
{: shortdesc}



```
ibmcloud oc logging-config-get --cluster CLUSTER [--logsource LOG_SOURCE] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--logsource <em>LOG_SOURCE</em></code></dt>
<dd>Il tipo di origine del log per la quale desideri eseguire il filtro. Vengono restituite le configurazioni di registrazione solo di questa origine del log nel cluster. I valori accettati sono <code>container</code>, <code>storage</code>, <code>application</code>, <code>worker</code>, <code>kubernetes</code>, <code>ingress</code> e <code>kube-audit</code>. Questo valore è facoltativo.</dd>

<dt><code>--show-covering-filters</code></dt>
<dd>Mostra i filtri di registrazione che rendono i precedenti filtri obsoleti.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc logging-config-get --cluster my_cluster --logsource worker
```
{: pre}

</br>
### `ibmcloud oc logging-config-refresh`
{: #cs_logging_refresh}

Aggiorna la configurazione di registrazione per il cluster. Questo azione aggiorna il token di registrazione per tutte le configurazioni di registrazione che stanno eseguendo l'inoltro al livello dello spazio nel tuo cluster.
{: shortdesc}



```
ibmcloud oc logging-config-refresh --cluster CLUSTER [--force-update] [-s]
```

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--force-update</code></dt>
<dd>Forza i tuoi pod Fluentd ad eseguire l'aggiornamento alla versione più recente. La versione di Fluentd deve essere la più recente per modificare le tue configurazioni di registrazione.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:

  ```
  ibmcloud oc logging-config-refresh --cluster my_cluster
  ```
  {: pre}

</br>
### `ibmcloud oc logging-config-rm`
{: #cs_logging_rm}

Elimina una configurazione di inoltro dei log o tutte le configurazioni di registrazione per un cluster. L'eliminazione della configurazione del log arresta l'inoltro del log a un server syslog remoto o a {{site.data.keyword.loganalysisshort_notm}}.
{: shortdesc}



```
ibmcloud oc logging-config-rm --cluster CLUSTER [--id LOG_CONFIG_ID] [--all] [--force-update] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster per tutte le origini log tranne `kube-audit` e ruolo della piattaforma **Amministratore** per il cluster per l'origine log `kube-audit`

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--id <em>LOG_CONFIG_ID</em></code></dt>
<dd>Se vuoi rimuovere una singola configurazione di registrazione, l'ID della configurazione di registrazione.</dd>

<dt><code>--all</code></dt>
<dd>L'indicatore per rimuovere tutte le configurazioni di registrazione in un cluster.</dd>

<dt><code>--force-update</code></dt>
<dd>Forza i tuoi pod Fluentd ad eseguire l'aggiornamento alla versione più recente. La versione di Fluentd deve essere la più recente per modificare le tue configurazioni di registrazione.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc logging-config-rm --cluster my_cluster --id f4bc77c0-ee7d-422d-aabf-a4e6b977264e
```
{: pre}

</br>
### `ibmcloud oc logging-config-update`
{: #cs_logging_update}

Aggiorna i dettagli di una configurazione di inoltro del log.
{: shortdesc}



```
ibmcloud oc logging-config-update --cluster CLUSTER --id LOG_CONFIG_ID --type LOG_TYPE  [--namespace NAMESPACE] [--hostname LOG_SERVER_HOSTNAME_OR_IP] [--port LOG_SERVER_PORT] [--space CLUSTER_SPACE] [--org CLUSTER_ORG] [--app-paths PATH] [--app-containers PATH] [--json] [--skipValidation] [--force-update] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--id <em>LOG_CONFIG_ID</em></code></dt>
<dd>L'ID di configurazione di registrazione che desideri aggiornare. Questo valore è obbligatorio.</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>Il protocollo di inoltro del log che desideri utilizzare. Al momento, sono supportati <code>syslog</code> e <code>ibm</code>. Questo valore è obbligatorio.</dd>

<dt><code>--namespace <em>NAMESPACE</em></code>
    <dd>Lo spazio dei nomi Kubernetes dal quale desideri inoltrare i log. L'inoltro del log non è supportato per gli spazi dei nomi Kubernetes <code>ibm-system</code> e <code>kube-system</code>. Questo valore è valido solo per l'origine log <code>container</code>. Se non specifichi uno spazio dei nomi, tutti gli spazi dei nomi nel cluster utilizzeranno questa configurazione.</dd>

<dt><code>--hostname <em>LOG_SERVER_HOSTNAME</em></code></dt>
<dd>Quando il tipo di registrazione è <code>syslog</code>, questo valore è il nome host o l'indirizzo IP del server di raccolta log. Questo valore è obbligatorio per <code>syslog</code>. Quando il tipo di registrazione è <code>ibm</code>, questo valore è l'URL di inserimento {{site.data.keyword.loganalysislong_notm}}. Puoi trovare l'elenco degli URL di inserimento disponibili [qui](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_ingestion#log_ingestion_urls). Se non specifichi un URL di inserimento, viene utilizzato l'endpoint della regione in cui è stato creato il tuo cluster.</dd>

<dt><code>--port <em>LOG_SERVER_PORT</em></code></dt>
<dd>La porta del server di raccolta del log. Questo valore è facoltativo quando il tipo di registrazione è <code>syslog</code>. Se non specifichi una porta, viene utilizzata la porta standard <code>514</code> per <code>syslog</code> e <code>9091</code> per <code>ibm</code>.</dd>

<dt><code>--space <em>CLUSTER_SPACE</em></code></dt>
<dd>Facoltativo: il nome dello spazio a cui vuoi inviare i log. Questo valore è valido solo per il tipo di log <code>ibm</code> ed è facoltativo. Se non specifichi uno spazio, i log vengono inviati al livello dell'account. Se lo specifichi, devi specificare anche un'<code>org</code>.</dd>

<dt><code>--org <em>CLUSTER_ORG</em></code></dt>
<dd>Facoltativo: il nome dell'organizzazione Cloud Foundry in cui si trova lo spazio. Questo valore è valido solo per il tipo di log <code>ibm</code> ed è obbligatorio se hai specificato uno spazio.</dd>

<dt><code>--app-paths <em>PATH</em>,<em>PATH</em></code></dt>
<dd>Un percorso file assoluto nel contenitore da cui raccogliere i log. Possono essere utilizzati i caratteri jolly, come '/var/log/*.log', ma non possono essere utilizzati i glob ricorrenti come '/var/log/**/test.log'. Per specificare più di un percorso, utilizza un elenco separato da virgole. Questo valore è obbligatorio quando specifichi 'application' per l'origine log. </dd>

<dt><code>--app-containers <em>PATH</em>,<em>PATH</em></code></dt>
<dd>Il percorso nei contenitori a cui si collegano le applicazioni. Per inoltrare i log con il tipo di origine <code>application</code>, devi fornire un percorso. Per specificare più di un percorso, utilizza un elenco separato da virgole. Esempio: <code>/var/log/myApp1/&ast;,/var/log/myApp2/&ast;</code></dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>--skipValidation</code></dt>
<dd>Ignora la convalida dei nomi di organizzazione e spazio quando vengono specificati. La mancata convalida riduce il tempo di elaborazione, ma una configurazione di registrazione non valida non inoltra correttamente i log. Questo valore è facoltativo.</dd>

<dt><code>--force-update</code></dt>
<dd>Forza i tuoi pod Fluentd ad eseguire l'aggiornamento alla versione più recente. La versione di Fluentd deve essere la più recente per modificare le tue configurazioni di registrazione.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio di tipo di log `ibm`**:

  ```
  ibmcloud oc logging-config-update my_cluster --id f4bc77c0-ee7d-422d-aabf-a4e6b977264e --type ibm
  ```
  {: pre}

**Esempio di tipo di log `syslog`**:

  ```
  ibmcloud oc logging-config-update --cluster my_cluster --id f4bc77c0-ee7d-422d-aabf-a4e6b977264e --hostname localhost --port 5514 --type syslog
  ```
  {: pre}

</br>
### `ibmcloud oc logging-filter-create`
{: #cs_log_filter_create}

Filtra i log inoltrati dalla tua configurazione della registrazione.
{: shortdesc}



```
ibmcloud oc logging-filter-create --cluster CLUSTER --type LOG_TYPE [--logging-configs CONFIGS] [--namespace KUBERNETES_NAMESPACE] [--container CONTAINER_NAME] [--level LOGGING_LEVEL] [--message MESSAGE] [--regex-message MESSAGE] [--force-update] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster per cui creare un filtro di registrazione. Questo valore è obbligatorio.</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>Il tipo di log a cui desideri applicare il filtro. Attualmente sono supportati <code>all</code>, <code>container</code> e <code>host</code>.</dd>

<dt><code>--logging-configs <em>CONFIGS</em></code></dt>
<dd>Un elenco separato da virgole dei tuoi ID di configurazione di registrazione. Se non viene fornito, il filtro viene applicato a tutte le configurazioni di registrazione cluster passate al filtro. Puoi visualizzare le configurazioni di registrazione che corrispondono al filtro utilizzando l'indicatore <code>--show-matching-configs</code> con il comando. Questo valore è facoltativo.</dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>Lo spazio dei nomi Kubernetes da cui desideri filtrare i log. Questo valore è facoltativo.</dd>

<dt><code>--container <em>CONTAINER_NAME</em></code></dt>
<dd>Il nome del contenitore da cui desideri filtrare i log. Questo indicatore si applica solo quando utilizzi il tipo di log <code>container</code>. Questo valore è facoltativo.</dd>

<dt><code>--level <em>LOGGING_LEVEL</em></code></dt>
<dd>Filtra i log che si trovano al livello specificato e a quelli inferiori ad esso. I valori accettabili nel loro ordine canonico sono <code>fatal</code>, <code>error</code>, <code>warn/warning</code>, <code>info</code>, <code>debug</code> e <code>trace</code>. Questo valore è facoltativo. Ad esempio, se hai filtrato i log a livello <code>info</code>, vengono filtrati anche <code>debug</code> e <code>trace</code>. **Nota**: puoi utilizzare questo indicatore solo quando i messaggi di log sono in formato JSON e contengono un campo di livello. Output di esempio: <code>{"log": "hello", "level": "info"}</code></dd>

<dt><code>--message <em>MESSAGE</em></code></dt>
<dd>Filtra i log che contengono un messaggio specificato in un qualsiasi punto nel log. Questo valore è facoltativo. Esempio: i messaggi "Hello", "!"e "Hello, World!"vengono applicati al log "Hello, World!".</dd>

<dt><code>--regex-message <em>MESSAGE</em></code></dt>
<dd>Filtra i log che contengono un messaggio specificato scritto come un'espressione regolare in un qualsiasi punto nel log. Questo valore è facoltativo. Esempio: il modello "hello [0-9]" viene applicato a "hello 1", "hello 2" e "hello 9".</dd>

<dt><code>--force-update</code></dt>
<dd>Forza i tuoi pod Fluentd ad eseguire l'aggiornamento alla versione più recente. La versione di Fluentd deve essere la più recente per modificare le tue configurazioni di registrazione.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempi**:

Questo esempio filtra tutti i log che sono stati inoltrati dai contenitori con il nome `test-container` nello spazio dei nomi predefinito che si trovano a livello debug o inferiore e che hanno un messaggio di log che contiene "GET request".
```
ibmcloud oc logging-filter-create --cluster example-cluster --type container --namespace default --container test-container --level debug --message "GET request"
```
{: pre}

Questo esempio filtra tutti i log che sono stati inoltrati, a un livello <code>info</code> o inferiore, da uno specifico cluster. L'output viene restituito come un JSON.
```
ibmcloud oc logging-filter-create --cluster example-cluster --type all --level info --json
```
{: pre}

</br>
### `ibmcloud oc logging-filter-get`
{: #cs_log_filter_view}

Visualizza la configurazione di un filtro di registrazione.
{: shortdesc}



```
ibmcloud oc logging-filter-get --cluster CLUSTER [--id FILTER_ID] [--show-matching-configs] [--show-covering-filters] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster dal quale desideri visualizzare i filtri. Questo valore è obbligatorio.</dd>

<dt><code>--id <em>FILTER_ID</em></code></dt>
<dd>L'ID del filtro di log che desideri visualizzare.</dd>

<dt><code>--show-matching-configs</code></dt>
<dd>Mostra le configurazioni di registrazione che corrispondono alla configurazione che stai visualizzando. Questo valore è facoltativo.</dd>

<dt><code>--show-covering-filters</code></dt>
<dd>Mostra i filtri di registrazione che rendono i precedenti filtri obsoleti. Questo valore è facoltativo.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc logging-filter-get --cluster mycluster --id 885732 --show-matching-configs
```
{: pre}

</br>
### `ibmcloud oc logging-filter-rm`
{: #cs_log_filter_delete}

Elimina un filtro di registrazione.
{: shortdesc}



```
ibmcloud oc logging-filter-rm --cluster CLUSTER [--id FILTER_ID] [--all] [--force-update] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster da cui desideri eliminare un filtro.</dd>

<dt><code>--id <em>FILTER_ID</em></code></dt>
<dd>L'ID del filtro di log da eliminare.</dd>

<dt><code>--all</code></dt>
<dd>Elimina tutti i tuoi filtri di inoltro del log. Questo valore è facoltativo.</dd>

<dt><code>--force-update</code></dt>
<dd>Forza i tuoi pod Fluentd ad eseguire l'aggiornamento alla versione più recente. La versione di Fluentd deve essere la più recente per modificare le tue configurazioni di registrazione.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc logging-filter-rm --cluster mycluster --id 885732
```
{: pre}

</br>
### `ibmcloud oc logging-filter-update`
{: #cs_log_filter_update}

Aggiorna un filtro di registrazione.
{: shortdesc}



```
ibmcloud oc logging-filter-update --cluster CLUSTER --id FILTER_ID --type LOG_TYPE [--logging-configs CONFIGS] [--namespace KUBERNETES_NAMESPACE] [--container CONTAINER_NAME] [--level LOGGING_LEVEL] [--message MESSAGE] [--regex-message MESSAGE] [--force-update] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster per il quale vuoi aggiornare un filtro di registrazione. Questo valore è obbligatorio.</dd>

<dt><code>--id <em>FILTER_ID</em></code></dt>
<dd>L'ID del filtro di log da aggiornare.</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>Il tipo di log a cui desideri applicare il filtro. Attualmente sono supportati <code>all</code>, <code>container</code> e <code>host</code>.</dd>

<dt><code>--logging-configs <em>CONFIGS</em></code></dt>
<dd>Un elenco separato da virgole dei tuoi ID di configurazione di registrazione. Se non viene fornito, il filtro viene applicato a tutte le configurazioni di registrazione cluster passate al filtro. Puoi visualizzare le configurazioni di registrazione che corrispondono al filtro utilizzando l'indicatore <code>--show-matching-configs</code> con il comando. Questo valore è facoltativo.</dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>Lo spazio dei nomi Kubernetes da cui desideri filtrare i log. Questo valore è facoltativo.</dd>

<dt><code>--container <em>CONTAINER_NAME</em></code></dt>
<dd>Il nome del contenitore da cui desideri filtrare i log. Questo indicatore si applica solo quando utilizzi il tipo di log <code>container</code>. Questo valore è facoltativo.</dd>

<dt><code>--level <em>LOGGING_LEVEL</em></code></dt>
<dd>Filtra i log che si trovano al livello specificato e a quelli inferiori ad esso. I valori accettabili nel loro ordine canonico sono <code>fatal</code>, <code>error</code>, <code>warn/warning</code>, <code>info</code>, <code>debug</code> e <code>trace</code>. Questo valore è facoltativo. Ad esempio, se hai filtrato i log a livello <code>info</code>, vengono filtrati anche <code>debug</code> e <code>trace</code>. **Nota**: puoi utilizzare questo indicatore solo quando i messaggi di log sono in formato JSON e contengono un campo di livello. Output di esempio: <code>{"log": "hello", "level": "info"}</code></dd>

<dt><code>--message <em>MESSAGE</em></code></dt>
<dd>Filtra i log che contengono un messaggio specificato in un qualsiasi punto nel log. Questo valore è facoltativo. Esempio: i messaggi "Hello", "!"e "Hello, World!"vengono applicati al log "Hello, World!".</dd>

<dt><code>--regex-message <em>MESSAGE</em></code></dt>
<dd>Filtra i log che contengono un messaggio specificato scritto come un'espressione regolare in un qualsiasi punto nel log. Questo valore è facoltativo. Esempio: il modello "hello [0-9]" viene applicato a "hello 1", "hello 2" e "hello 9"</dd>

<dt><code>--force-update</code></dt>
<dd>Forza i tuoi pod Fluentd ad eseguire l'aggiornamento alla versione più recente. La versione di Fluentd deve essere la più recente per modificare le tue configurazioni di registrazione.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempi**:

Questo esempio filtra tutti i log che sono stati inoltrati dai contenitori con il nome `test-container` nello spazio dei nomi predefinito che si trovano a livello debug o inferiore e che hanno un messaggio di log che contiene "GET request".
```
ibmcloud oc logging-filter-update --cluster example-cluster --id 885274 --type container --namespace default --container test-container --level debug --message "GET request"
```
{: pre}

Questo esempio filtra tutti i log che sono stati inoltrati, a un livello <code>info</code> o inferiore, da uno specifico cluster. L'output viene restituito come un JSON.
```
ibmcloud oc logging-filter-update --cluster example-cluster --id 274885 --type all --level info --json
```
{: pre}

<br />


## Comandi NLB (network load balancer)
{: #nlb-dns}

Utilizza questo gruppo di comandi per creare e gestire nomi host per indirizzi IP NLB (network load balancer) e i monitoraggi del controllo di integrità per i nomi host. Per ulteriori informazioni, vedi [Registrazione del nome di un host di bilanciamento del carico](/docs/containers?topic=containers-loadbalancer_hostname).
{: shortdesc}



### `ibmcloud oc nlb-dns-add`
{: #cs_nlb-dns-add}

Aggiungi un IP NLB (network load balancer) a un nome host esistente che hai creato con il [comando `ibmcloud oc nlb-dns-create`](#cs_nlb-dns-create).
{: shortdesc}



Ad esempio, in un cluster multizona, potresti creare un NLB in ciascuna zona per esporre un'applicazione. Registri un IP NLB in una zona con un nome host, eseguendo `ibmcloud oc nlb-dns-create`, quindi ora puoi aggiungere gli IP NLB delle altre zone a questo nome host esistente. Quando un utente accede al nome host della tua applicazione, il client accede a uno di questi IP a caso e la richiesta viene inviata a tale NLB. Devi eseguire il seguente comando per ciascun indirizzo IP che desideri aggiungere.

```
ibmcloud oc nlb-dns-add --cluster CLUSTER --ip IP --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--ip <em>IP</em></code></dt>
<dd>L'IP NLB che vuoi aggiungere al nome host. Per visualizzare i tuoi IP NLB, esegui <code>oc get svc</code>.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Il nome host a cui desideri aggiungere gli IP. Per visualizzare i nomi host esistenti, esegui <code>ibmcloud oc nlb-dnss</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dns-add --cluster mycluster --ip 1.1.1.1 --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-create`
{: #cs_nlb-dns-create}

Esponi pubblicamente la tua applicazione creando un nome host DNS per registrare un IP NLB (network load balancer).
{: shortdesc}



```
ibmcloud oc nlb-dns-create --cluster CLUSTER --ip IP [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--ip <em>IP</em></code></dt>
<dd>L'indirizzo IP NLB che desideri registrare. Per visualizzare i tuoi IP NLB, esegui <code>oc get svc</code>.Puoi inizialmente creare il nome host con un solo indirizzo IP. Se disponi di NLB in ciascuna zona di un cluster multizona che espongono una sola applicazione, puoi aggiungere gli IP degli altri NLB al nome host eseguendo il comando [`ibmcloud oc nlb-dns-add`.](#cs_nlb-dns-add).</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dns-create --cluster mycluster --ip 1.1.1.1
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-rm`
{: #cs_nlb-dns-rm}

Rimuovi un indirizzo IP NLB da un nome host. Se rimuovi tutti gli IP da un nome host, il nome host esiste ancora, ma non è associato ad alcun IP. <strong>Nota</strong>: devi eseguire questo comando per ogni indirizzo IP che vuoi rimuovere.
{: shortdesc}



```
ibmcloud oc nlb-dns-rm --cluster CLUSTER --ip IP --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--ip <em>IP</em></code></dt>
<dd>L'IP NLB che desideri rimuovere. Per visualizzare i tuoi IP NLB, esegui <code>oc get svc</code>.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Il nome host da cui desideri rimuovere un IP. Per visualizzare i nomi host esistenti, esegui <code>ibmcloud oc nlb-dnss</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dns-rm --cluster mycluster --ip 1.1.1.1 --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>
### `ibmcloud oc nlb-dnss`
{: #cs_nlb-dns-ls}

Elenca i nomi host NLB e gli indirizzi IP registrati in un cluster.
{: shortdesc}



```
ibmcloud oc nlb-dnss --cluster CLUSTER [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dnss --cluster mycluster
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-monitor-configure`
{: #cs_nlb-dns-monitor-configure}

Configura e abilita, facoltativamente, un monitoraggio del controllo di integrità per un nome host NLB esistente in un cluster. Quando abiliti un monitoraggio per il tuo nome host, esso controlla lo stato di integrità dell'IP NLB in ciascuna zona e mantiene aggiornati i risultati della ricerca DNS sulla base dei controlli di integrità effettuati.
{: shortdesc}

Puoi utilizzare questo comando per creare e abilitare un nuovo monitoraggio del controllo di integrità o per aggiornare le impostazioni di un monitoraggio del controllo di integrità esistente. Per creare un nuovo monitoraggio, includi l'indicatore `-- enable` e indicatori per tutte le impostazioni che desideri configurare. Per aggiornare un monitoraggio esistente, includi solo gli indicatori per le impostazioni che desideri modificare.



```
ibmcloud oc nlb-dns-monitor-configure --cluster CLUSTER --nlb-host HOST NAME [--enable] [--desc DESCRIPTION] [--type TYPE] [--method METHOD] [--path PATH] [--timeout TIMEOUT] [--retries RETRIES] [--interval INTERVAL] [--port PORT] [--header HEADER] [--expected-body BODY STRING] [--expected-codes HTTP CODES] [--follows-redirects TRUE] [--allows-insecure TRUE] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster in cui è registrato il nome host.</dd>

<dt><code>--nlb-host <em>HOST NAME</em></code></dt>
<dd>Il nome host per cui configurare un monitoraggio del controllo di integrità. Per elencare i nomi host, esegui <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--enable</code></dt>
<dd>Includi questo indicatore per creare e abilitare un nuovo monitoraggio del controllo di integrità per un nome host.</dd>

<dt><code>--description <em>DESCRIPTION</em></code></dt>
<dd>Descrizione del monitoraggio dell'integrità.</dd>

<dt><code>--type <em>TYPE</em></code></dt>
<dd>Il protocollo da utilizzare per il controllo di integrità: <code>HTTP</code>, <code>HTTPS</code> o <code>TCP</code>. Impostazione predefinita: <code>HTTP</code></dd>

<dt><code>--method <em>METHOD</em></code></dt>
<dd>Metodo da utilizzare per il controllo di integrità. Impostazione predefinita per il <code>type</code> <code>HTTP</code> e <code>HTTPS</code>: <code>GET</code>. Impostazione predefinita per il<code>type</code> <code>TCP</code>: <code>connection_established</code>.</dd>

<dt><code>--path <em>PATH</em></code></dt>
<dd>Quando il <code>type</code> è <code>HTTPS</code>: il percorso dell'endpoint per cui viene eseguito il controllo di integrità. Impostazione predefinita: <code>/</code></dd>

<dt><code>--timeout <em>TIMEOUT</em></code></dt>
<dd>Il timeout, in secondi, prima che l'IP venga considerato irraggiungibile. Il controllo di integrità attende il numero di secondi specificato nel parametro `interval` prima di provare nuovamente a raggiungere l'IP. Il valore deve essere un numero intero compreso nell'intervallo 1 - 15. Impostazione predefinita: <code>5</code></dd>

<dt><code>--retries <em>RETRIES</em></code></dt>
<dd>Quando si verifica un timeout, il numero di tentativi da eseguire prima che l'IP irraggiungibile venga considerato non integro. I nuovi tentativi vengono effettuati immediatamente. Il valore deve essere un numero intero compreso nell'intervallo 1 - 5. Impostazione predefinita: <code>2</code></dd>

<dt><code>--interval <em>INTERVAL</em></code></dt>
<dd>Intervallo, in secondi, tra ogni controllo di integrità. L'uso di intervalli brevi potrebbe diminuire il tempo di failover, ma aumentare il carico sugli IP. Il valore deve essere un numero intero compreso nell'intervallo 10 - 3600 e deve essere più grande di `(RETRIES + 1) * TIMEOUT`. Impostazione predefinita: <code>60</code></dd>

<dt><code>--port <em>PORT</em></code></dt>
<dd>Il numero di porta a cui connettersi per il controllo di integrità. Se <code>type</code> è <code>TCP</code>, questo parametro è obbligatorio. Se <code>type</code> è <code>HTTP</code> o <code>HTTPS</code>, definisci la porta solo se utilizzi una porta diversa da 80 per HTTP o 443 per HTTPS. Valore predefinito per il TCP: <code>0</code>. Valore predefinito per l'HTTP: <code>80</code>. Valore predefinito per l'HTTPS: <code>443</code>.</dd>

<dt><code>--header <em>HEADER</em></code></dt>
<dd>Se il <code>type</code> è <code>HTTPS</code> o <code>HTTPS</code>: le intestazioni delle richieste HTTP da inviare nel controllo di integrità, come ad esempio un'intestazione Host. L'intestazione User-Agent non può essere sovrascritta.</dd>

<dt><code>--expected-body <em>BODY STRING</em></code></dt>
<dd>Quando il <code>type</code> è <code>HTTP</code> o <code>HTTPS</code>: una stringa secondaria senza distinzione di maiuscole/minuscole che il controllo di integrità ricerca nel corpo della risposta. Se
questa stringa non viene trovata, l'IP viene considerato non integro.</dd>

<dt><code>--expected-codes <em>HTTP CODES</em></code></dt>
<dd>Se il <code>type</code> è <code>HTTP</code> o <code>HTTPS</code>: codici HTTP che il controllo di integrità ricerca nella risposta. Se il codice HTTP non viene trovato, l'IP viene considerato non integro. Impostazione predefinita: <code>2xx</code></dd>

<dt><code>--allows-insecure <em>TRUE</em></code></dt>
<dd>Se il <code>type</code> è <code>HTTP</code> o <code>HTTPS</code>: impostalo su <code>true</code> per non convalidare il certificato.</dd>

<dt><code>--follows-redirects <em>TRUE</em></code></dt>
<dd>Se il <code>type</code> è <code>HTTP</code> o <code>HTTPS</code>: impostalo su <code>true</code> per seguire i reindirizzamenti restituiti dall'IP.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dns-monitor-configure --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud --enable --desc "Login page monitor" --type HTTPS --method GET --path / --timeout 5 --retries 2 --interval 60  --expected-body "healthy" --expected-codes 2xx --follows-redirects true
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-monitor-disable`
{: #cs_nlb-dns-monitor-disable}

Disabilita un monitoraggio del controllo di integrità esistente per un nome host in un cluster.
{: shortdesc}



```
ibmcloud oc nlb-dns-monitor-disable --cluster CLUSTER --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Il nome host per cui il monitoraggio effettua il controllo di integrità. Per elencare i nomi host, esegui <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dns-monitor-disable --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-monitor-enable`
{: #cs_nlb-dns-monitor-enable}

Abilita un monitoraggio del controllo di integrità che hai configurato.
{: shortdesc}

La prima volta che crei un monitoraggio di un controllo di integrità, devi configurarlo e abilitarlo con il comando `ibmcloud oc nlb-dns-monitor-configure`. Utilizza il comando `ibmcloud oc nlb-dns-monitor-enable` solo per abilitare un monitor che hai configurato, ma non ancora abilitato, o per riabilitare un monitor che hai disabilitato in precedenza.



```
ibmcloud oc nlb-dns-monitor-enable --cluster CLUSTER --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Il nome host per cui il monitoraggio effettua il controllo di integrità. Per elencare i nomi host, esegui <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dns-monitor-enable --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>

### `ibmcloud oc nlb-dns-monitor-get`
{: #cs_nlb-dns-monitor-get}

Visualizza le impostazioni per un monitoraggio del controllo di integrità esistente.
{: shortdesc}



```
ibmcloud oc nlb-dns-monitor-get --cluster CLUSTER --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Il nome host per cui il monitoraggio effettua il controllo di integrità. Per elencare i nomi host, esegui <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dns-monitor-get --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>

### `ibmcloud oc nlb-dns-monitor-status`
{: #cs_nlb-dns-monitor-status}

Elenca lo stato del controllo di integrità degli IP che stanno dietro i nomi host NLB di un cluster.
{: shortdesc}



```
ibmcloud oc nlb-dns-monitor-status --cluster CLUSTER [--nlb-host HOST_NAME] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Includi questo indicatore per visualizzare lo stato di un solo nome host. Per elencare i nomi host, esegui <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dns-monitor-status --cluster mycluster
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-monitors`
{: #cs_nlb-dns-monitor-ls}

Elenca le impostazioni del monitoraggio del controllo di integrità per ciascun nome host NLB di un cluster.
{: shortdesc}



```
ibmcloud oc nlb-dns-monitors --cluster CLUSTER [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Editor** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc nlb-dns-monitors --cluster mycluster
```
{: pre}

<br />


## Comandi della regione e dell'ubicazione
{: #region_commands}

Utilizza questo gruppo di comandi per visualizzare le località disponibili, visualizzare la regione di destinazione attuale e impostare la regione di destinazione.
{: shortdesc}

### Obsoleto: `ibmcloud oc region-get`
{: #cs_region}

Trova la regione {{site.data.keyword.containerlong_notm}} a cui sei attualmente assegnato.
{: shortdesc}

Puoi gestire le risorse a cui hai accesso in qualsiasi ubicazione, anche se imposti una regione eseguendo `ibmcloud oc region-set` e la risorsa che vuoi gestire si trova in un'altra regione. Se hai dei cluster con lo stesso nome in regioni differenti, puoi utilizzare l'ID cluster quando esegui i comandi o impostare una regione con il comando `ibmcloud oc region-set` e utilizzare il nome cluster quando esegui i comandi.

<p class="deprecated">Modalità di funzionamento legacy:</br>se utilizzi il plugin {{site.data.keyword.containerlong_notm}} versione <code>0.3</code> o successive e devi elencare e gestire le risorse solo da una singola regione, puoi utilizzare il [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_init) <code>ibmcloud oc init</code> per indicare come destinazione un endpoint regionale invece dell'endpoint globale.</br>Se [imposti la variabile di ambiente <code>IKS_BETA_VERSION</code> nel plugin {{site.data.keyword.containerlong_notm}} su <code>0.2</code>](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_beta), crei e gestisci i cluster specifici per la regione. Utilizza il comando <code>ibmcloud oc region-set</code> per modificare le regioni.</p>

```
ibmcloud oc region-get
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

</br>
### Obsoleto: `ibmcloud oc region-set`
{: #cs_region-set}

Imposta la regione per {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

Puoi gestire le risorse a cui hai accesso in qualsiasi ubicazione, anche se imposti una regione eseguendo `ibmcloud oc region-set` e la risorsa che vuoi gestire si trova in un'altra regione. Se hai dei cluster con lo stesso nome in regioni differenti, puoi utilizzare l'ID cluster quando esegui i comandi o impostare una regione con il comando `ibmcloud oc region-set` e utilizzare il nome cluster quando esegui i comandi.

Se utilizzi la versione `0.2` beta (legacy) del plug-in {{site.data.keyword.containerlong_notm}}, crei e gestisci i cluster specifici per la regione. Ad esempio, puoi accedere a {{site.data.keyword.cloud_notm}} nella regione Stati Uniti Sud e creare un cluster. Successivamente, puoi utilizzare `ibmcloud oc region-set eu-central` per indicare come destinazione la regione Europa Centrale e creare un altro cluster. Infine, puoi utilizzare `ibmcloud oc region-set us-south` per ritornare alla regione Stati Uniti Sud per gestire il tuo cluster in tale regione.
{: deprecated}

```
ibmcloud oc region-set --region REGION
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

**Opzioni comando**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Immetti la regione che vuoi specificare. Questo valore è facoltativo. Se non fornisci la regione, puoi selezionarla dall'elenco nell'output.

Per un elenco delle regioni disponibili, riesamina [Ubicazioni](/docs/containers?topic=containers-regions-and-zones) oppure utilizza il [comando](#cs_regions) `ibmcloud oc regions`.</dd></dl>

**Esempio**:
```
ibmcloud oc region-set --region eu-central
```
{: pre}

</br>
### Obsoleto: `ibmcloud oc regions`
{: #cs_regions}

Elenca le regioni disponibili. `Region Name` è il nome {{site.data.keyword.containerlong_notm}} e `Region Alias` è il nome {{site.data.keyword.cloud_notm}} generale della regione.
{: shortdesc}

Gli endpoint specifici per la regione sono stati dichiarati obsoleti. Utilizza invece l'[endpoint globale](/docs/containers?topic=containers-regions-and-zones#endpoint).
{: deprecated}

**Autorizzazioni minime richieste**: nessuna

**Esempio**:
```
ibmcloud oc regions
```
{: pre}

**Output**:
```
Region Name   Region Alias
ap-north      jp-tok
ap-south      au-syd
eu-central    eu-de
uk-south      eu-gb
us-east       us-east
us-south      us-south
```
{: screen}

</br>
### `ibmcloud oc supported-locations`
{: #cs_supported-locations}

Elenca le ubicazioni che sono supportate da {{site.data.keyword.containerlong_notm}}. Per ulteriori informazioni sulle ubicazioni restituite, vedi [Ubicazioni di {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-regions-and-zones#locations).
{: shortdesc}



```
ibmcloud oc supported-locations
```
{: pre}

**Autorizzazioni minime richieste**: nessuna

</br>
### `ibmcloud oc zones`
{: #cs_datacenters}

Visualizza un elenco delle zone disponibili in cui puoi creare un cluster.
{: shortdesc}



Se utilizzi la versione `0.2` beta (legacy) del plug-in {{site.data.keyword.containerlong_notm}}, le zone disponibili variano in base alla regione a cui hai eseguito l'accesso. Per passare da una regione a un'altra, esegui `ibmcloud oc region-set`.
{: deprecated}

```
ibmcloud oc zones [--locations LOCATION] [--region-only] [--json] [-s]
```
{: pre}

**Autorizzazioni minime**: nessuna

**Opzioni comando**:
<dl>
<dt><code>--locations <em>LOCATION</em></code></dt>
<dd>Filtra le zone in base a una specifica ubicazione o a un elenco di ubicazioni separate da virgole. Per visualizzare le ubicazioni supportate, esegui <code>ibmcloud oc supported-locations</code>.</dd>

<dt><code>--region-only</code></dt>
<dd>Elenca solo gli elementi multizona all'interno della regione a cui hai eseguito l'accesso. Questo valore è facoltativo.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc zones --locations ap
```
{: pre}

<br />



## Comandi nodo di lavoro
{: worker_node_commands}

### Obsoleto: `ibmcloud oc worker-add`
{: #cs_worker_add}

Aggiungi dei nodi di lavoro autonomi a un cluster.
{: shortdesc}

Questo comando è stato dichiarato obsoleto. Crea un pool di nodi di lavoro eseguendo [`ibmcloud oc worker-pool-create`](#cs_worker_pool_create) oppure aggiungi i nodi di lavoro a un pool di nodi di lavoro esistente eseguendo [`ibmcloud oc worker-pool-resize`](#cs_worker_pool_resize).
{: deprecated}

```
ibmcloud oc worker-add --cluster CLUSTER [--file FILE_LOCATION] [--hardware HARDWARE] --machine-type MACHINE_TYPE --workers NUMBER --private-vlan PRIVATE_VLAN --public-vlan PUBLIC_VLAN [--disable-disk-encrypt] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--file <em>FILE_LOCATION</em></code></dt>
<dd>Il percorso al file YAML per aggiungere i nodi di lavoro al cluster. Invece di definire ulteriori nodi di lavoro utilizzando le opzioni fornite in questo comando, puoi utilizzare un file YAML. Questo valore è facoltativo.

<p class="note">Se fornisci la stessa opzione nel comando come parametro nel file YAML, il valore nel comando ha la precedenza rispetto al valore nel file YAML. Ad esempio, definisci un profilo nel tuo file YAML e utilizzi l'opzione <code>--machine-type</code> nel comando; il valore che hai immesso nell'opzione del comando sovrascrive il valore nel file YAML.</p>

<pre class="codeblock">
<code>name: <em>&lt;cluster_name_or_ID&gt;</em>
zone: <em>&lt;zone&gt;</em>
machine-type: <em>&lt;machine_type&gt;</em>
private-vlan: <em>&lt;private_VLAN&gt;</em>
public-vlan: <em>&lt;public_VLAN&gt;</em>
hardware: <em>&lt;shared_or_dedicated&gt;</em>
workerNum: <em>&lt;number_workers&gt;</em>
diskEncryption: <em>false</em></code></pre>

<table>
<caption>Descrizione dei componenti del file YAML</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Icona Idea"/> Descrizione dei componenti del file YAML</th>
</thead>
<tbody>
<tr>
<td><code><em>name</em></code></td>
<td>Sostituisci <code><em>&lt;cluster_name_or_ID&gt;</em></code> con il nome o l'ID del cluster in cui desideri aggiungere nodi di lavoro.</td>
</tr>
<tr>
<td><code><em>zone</em></code></td>
<td>Sostituisci <code><em>&lt;zone&gt;</em></code> con la zona in cui distribuire i tuoi nodi di lavoro. Le zone disponibili dipendono dalla regione a cui hai eseguito l'accesso. Per elencare le zone disponibili, esegui <code>ibmcloud oc zones</code>.</td>
</tr>
<tr>
<td><code><em>machine-type</em></code></td>
<td>Sostituisci <code><em>&lt;machine_type&gt;</em></code> con il profilo, o il tipo di macchina a cui vuoi distribuire i tuoi nodi di lavoro. Puoi distribuire i tuoi nodi di lavoro come macchine virtuali su hardware condiviso o dedicato o come macchine fisiche su bare metal. I profili fisici e virtuali disponibili variano in base alla zona in cui distribuisci il cluster. Per ulteriori informazioni, vedi il [comando](#cs_machine_types) `ibmcloud oc flavors (machine-types)`.</td>
</tr>
<tr>
<td><code><em>private-vlan</em></code></td>
<td>Sostituisci <code><em>&lt;private_VLAN&gt;</em></code> con l'ID della VLAN privata che vuoi utilizzare per i tuoi nodi di lavoro. Per elencare le VLAN disponibili, esegui <code>ibmcloud oc vlans --zone <em>&lt;zone&gt;</em></code> e cerca i router VLAN che iniziano con <code>bcr</code> (back-end router).</td>
</tr>
<tr>
<td><code>public-vlan</code></td>
<td>Sostituisci <code>&lt;public_VLAN&gt;</code> con l'ID della VLAN pubblica che vuoi utilizzare per i tuoi nodi di lavoro. Per elencare le VLAN disponibili, esegui <code>ibmcloud oc vlans --zone &lt;zone&gt;</code> e cerca i router VLAN che iniziano con <code>fcr</code> (front-end router).<br><strong>Nota</strong>: se i nodi di lavoro sono configurati solo con una VLAN privata, devi consentire le comunicazioni tra i nodi di lavoro e il master cluster [abilitando l'endpoint del servizio privato](/docs/containers?topic=containers-cs_network_cluster#set-up-private-se) oppure [configurando un dispositivo gateway](/docs/containers?topic=containers-plan_clusters#workeruser-master).</td>
</tr>
<tr>
<td><code>hardware</code></td>
<td>Per i profili virtuali: il livello di isolamento hardware per il tuo nodo di lavoro. Utilizza `dedicated` in modo che le risorse fisiche disponibili siano dedicate solo a te oppure `shared` per consentire la condivisione delle risorse fisiche con altri clienti IBM. L'impostazione predefinita è
`shared`.</td>
</tr>
<tr>
<td><code>workerNum</code></td>
<td>Sostituisci <code><em>&lt;number_workers&gt;</em></code> con il numero di nodi di lavoro che vuoi distribuire.</td>
</tr>
<tr>
<td><code>diskEncryption: <em>false</em></code></td>
<td>I nodi di lavoro sono dotati di crittografia disco AES a 256 bit per impostazione predefinita; [ulteriori informazioni](/docs/containers?topic=containers-security#encrypted_disk). Per disabilitare la crittografia, includi questa opzione e imposta il valore su <code>false</code>.</td></tr>
</tbody></table></p></dd>

<dt><code>--hardware <em>HARDWARE</em></code></dt>
<dd>Il livello di isolamento hardware per il nodo di lavoro. Utilizza `dedicated` in modo che le risorse fisiche disponibili siano dedicate solo a te oppure `shared` per consentire la condivisione delle risorse fisiche con altri clienti IBM. L'impostazione predefinita è
`shared`. Questo valore è facoltativo. Per i profili bare metal, specifica `dedicated`.</dd>

<dt><code>--machine-type <em>MACHINE_TYPE</em></code></dt>
<dd>Scegli un tipo di macchina, o un profilo, per i tuoi nodi di lavoro. Puoi distribuire i tuoi nodi di lavoro come macchine virtuali su hardware condiviso o dedicato o come macchine fisiche su bare metal. I tipi di macchine fisiche e virtuali disponibili variano in base alla zona in cui distribuisci il cluster. Per ulteriori informazioni, vedi la documentazione per il [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_machine_types) `ibmcloud oc flavors (machine-types)`. Questo valore è obbligatorio per i cluster standard e non è disponibile per i cluster gratuiti.</dd>

<dt><code>--workers <em>NUMBER</em></code></dt>
<dd>Un numero intero che rappresenta il numero di nodi di lavoro da creare nel cluster. Il valore predefinito è 1. Questo valore è facoltativo.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>La VLAN privata specificata quando è stato creato il cluster. Questo valore è obbligatorio. I router della VLAN privata iniziano sempre con <code>bcr</code> (router back-end) e i router della VLAN pubblica iniziano sempre con <code>fcr</code> (router front-end). Quando crei un cluster e specifichi le VLAN pubbliche e private, la combinazione di numeri e lettere dopo tali prefissi devono corrispondere.</dd>

<dt><code>--public-vlan <em>PUBLIC_VLAN</em></code></dt>
<dd>La VLAN pubblica specificata quando è stato creato il cluster. Questo valore è facoltativo. Se vuoi che i tuoi nodi di lavoro siano solo su una VLAN privata, non fornire un ID VLAN pubblico. I router della VLAN privata iniziano sempre con <code>bcr</code> (router back-end) e i router della VLAN pubblica iniziano sempre con <code>fcr</code> (router front-end). Quando crei un cluster e specifichi le VLAN pubbliche e private, la combinazione di numeri e lettere dopo tali prefissi devono corrispondere.<p class="note">Se i nodi di lavoro sono configurati solo con una VLAN privata, devi consentire le comunicazioni tra i nodi di lavoro e il master cluster [abilitando l'endpoint del servizio privato](/docs/containers?topic=containers-cs_network_cluster#set-up-private-se) o [configurando un dispositivo gateway](/docs/containers?topic=containers-plan_clusters#workeruser-master).</p></dd>

<dt><code>--disable-disk-encrypt</code></dt>
<dd>I nodi di lavoro sono dotati di crittografia disco AES a 256 bit per impostazione predefinita; [ulteriori informazioni](/docs/containers?topic=containers-security#encrypted_disk). Per disabilitare la crittografia, includi questa opzione.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>

</dl>

**Esempio**:
```
ibmcloud oc worker-add --cluster my_cluster --workers 3 --public-vlan my_public_VLAN_ID --private-vlan my_private_VLAN_ID --machine-type b3c.4x16 --hardware shared
```
{: pre}

</br>
### `ibmcloud oc worker-get`
{: #cs_worker_get}

Visualizza i dettagli di un nodo di lavoro.
{: shortdesc}



```
ibmcloud oc worker-get --cluster CLUSTER_NAME_OR_ID --worker WORKER_NODE_ID [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER_NAME_OR_ID</em></code></dt>
<dd>Il nome o l'ID del cluster del nodo di lavoro. Questo valore è facoltativo.</dd>

<dt><code>--worker <em>WORKER_NODE_ID</em></code></dt>
<dd>Il nome del tuo nodo di lavoro. Esegui <code>ibmcloud oc workers --cluster <em>CLUSTER</em></code> per visualizzare gli ID per i nodi di lavoro in un cluster. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-get --cluster my_cluster --worker kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1
```
{: pre}

**Output di esempio**:

  ```
  ID:           kube-dal10-123456789-w1
  State:        normal
  Status:       Ready
  Trust:        disabled
  Private VLAN: 223xxxx
  Public VLAN:  223xxxx
  Private IP:   10.xxx.xx.xxx
  Public IP:    169.xx.xxx.xxx
  Hardware:     shared
  Zone:         dal10
  Version:      1.8.11_1509
  ```
  {: screen}

</br>
### `ibmcloud oc worker-reboot`
{: #cs_worker_reboot}

Riavvia un nodo di lavoro in un cluster.
{: shortdesc}



Durante il riavvio, lo stato del tuo nodo di lavoro non cambia. Ad esempio, potresti utilizzare un riavvio se lo stato del nodo di lavoro nell'infrastruttura IBM Cloud è `Powered Off` e hai bisogno di attivare il nodo di lavoro. Un riavvio cancella le directory temporanee, ma non cancella l'intero file system o riformatta i dischi. L'indirizzo IP del nodo di lavoro rimane lo stesso dopo l'operazione di riavvio.

Il riavvio di un nodo di lavoro può causare il danneggiamento dei dati sul nodo di lavoro. Utilizza questo comando con cautela e quando sai che un riavvio può aiutare a ripristinare il tuo nodo di lavoro. In tutti gli altri casi, [ricarica il tuo nodo di lavoro](#cs_worker_reload).
{: important}

Prima di riavviare il tuo nodo di lavoro, assicurati che i pod vengano ripianificati su altri nodi di lavoro per evitare un periodo di inattività per la tua applicazione o il danneggiamento dei dati sul nodo di lavoro.

1. Elenca tutti i nodi di lavoro presenti nel tuo cluster e prendi nota del **nome** del nodo di lavoro che vuoi rimuovere.
   ```
   oc get nodes
   ```
   {: pre}
   Il **nome** che viene restituito in questo comando è l'indirizzo IP privato che è assegnato al tuo nodo di lavoro. Puoi trovare ulteriori informazioni sul tuo nodo di lavoro eseguendo il comando `ibmcloud oc workers --cluster <cluster_name_or_ID>` e cercando il nodo di lavoro con lo stesso indirizzo **IP privato**.

2. Contrassegna il nodo di lavoro come non pianificabile in un processo noto come delimitazione. Quando delimiti un nodo di lavoro, lo rendi non disponibile per una futura pianificazione di pod. Utilizza il **nome** del nodo di lavoro che hai richiamato nel passo precedente.
   ```
   oc cordon <worker_name>
   ```
   {: pre}

3. Verifica che la pianificazione di pod sia disabilitata per il tuo nodo di lavoro.
   ```
   oc get nodes
   ```
   {: pre}
   Il tuo nodo di lavoro è disabilitato per la pianificazione di pod se lo stato visualizza **SchedulingDisabled**.

4. Forza la rimozione dei pod dal tuo nodo di lavoro e la loro ripianificazione sui nodi di lavoro rimanenti nel cluster.
  ```
  oc drain <worker_name>
  ```
  {: pre}
  Questo processo può richiedere qualche minuto.
5. Riavvia il nodo di lavoro. Utilizza l'ID nodo di lavoro restituito dal comando `ibmcloud oc workers --cluster <cluster_name_or_ID>`.
  ```
  ibmcloud oc worker-reboot --cluster <cluster_name_or_ID> --workers <worker_name_or_ID>
  ```
  {: pre}
6. Attendi circa 5 minuti prima di rendere disponibile il tuo nodo di lavoro per la pianificazione di pod per assicurarti che il riavvio sia terminato. Durante il riavvio, lo stato del tuo nodo di lavoro non cambia. Il riavvio di un nodo di lavoro viene in genere completato in pochi secondi.
7. Rendi disponibile il tuo nodo di lavoro per la pianificazione di pod. Utilizza il **nome** per il tuo nodo di lavoro restituito dal comando `oc get nodes`.
  ```
  oc uncordon <worker_name>
  ```
  {: pre}

  </br>

```
ibmcloud oc worker-reboot [-f] [--hard] --cluster CLUSTER --worker WORKER [WORKER] [--skip-master-healthcheck] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>-f</code></dt>
<dd>Utilizza questa opzione per forzare il riavvio del nodo di lavoro senza richiedere l'intervento dell'utente. Questo valore è facoltativo.</dd>

<dt><code>--hard</code></dt>
<dd>Utilizza questa opzione per effettuare un riavvio forzato di un nodo di lavoro togliendo l'alimentazione al nodo di lavoro. Utilizza questa opzione se il nodo di lavoro non risponde o se il runtime del contenitore del nodo di lavoro non risponde. Questo valore è facoltativo.</dd>

<dt><code>--workers <em>WORKER</em></code></dt>
<dd>Il nome o l'ID di uno o più nodi di lavoro. Utilizza uno spazio per elencare più nodi di lavoro. Questo valore è obbligatorio.</dd>

<dt><code>--skip-master-healthcheck</code></dt>
<dd>Ignora un controllo di integrità del tuo master prima di ricaricare o riavviare i nodi di lavoro.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-reboot --cluster my_cluster --worker kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>
### `ibmcloud oc worker-reload`
{: #cs_worker_reload}

Ricarica le configurazioni per un nodo di lavoro.
{: shortdesc}



Un ricaricamento può essere utile se il tuo nodo di lavoro riscontra dei problemi, come prestazioni scarse o se il nodo di lavoro è bloccato in uno stato non integro. Durante il ricaricamento, la macchina del nodo di lavoro viene aggiornata con l'immagine più recente e i dati vengono eliminati se non sono [archiviati all'esterno del nodo di lavoro](/docs/containers?topic=containers-storage_planning#persistent_storage_overview). L'indirizzo IP pubblico e quello privato del nodo di lavoro rimangono gli stessi dopo l'operazione di ricaricamento.

Il ricaricamento di un nodo di lavoro viene applicato agli aggiornamenti della versione patch per il tuo nodo di lavoro, ma non per aggiornamenti maggiori o minori. Per visualizzare le modifiche da un versione patch alla successiva, controlla la documentazione [Changelog versione](/docs/containers?topic=containers-changelog#changelog).
{: tip}

Prima di ricaricare il tuo nodo di lavoro, assicurati che i pod vengano ripianificati su altri nodi di lavoro per evitare un periodo di inattività per la tua applicazione o il danneggiamento dei dati sul nodo di lavoro.

1. Elenca tutti i nodi di lavoro presenti nel tuo cluster e prendi nota del **nome** del nodo di lavoro che vuoi ricaricare.
   ```
   oc get nodes
   ```
   Il **nome** che viene restituito in questo comando è l'indirizzo IP privato che è assegnato al tuo nodo di lavoro. Puoi trovare ulteriori informazioni sul tuo nodo di lavoro eseguendo il comando `ibmcloud oc workers --cluster <cluster_name_or_ID>` e cercando il nodo di lavoro con lo stesso indirizzo **IP privato**.
2. Contrassegna il nodo di lavoro come non pianificabile in un processo noto come delimitazione. Quando delimiti un nodo di lavoro, lo rendi non disponibile per una futura pianificazione di pod. Utilizza il **nome** del nodo di lavoro che hai richiamato nel passo precedente.
   ```
   oc cordon <worker_name>
   ```
   {: pre}

3. Verifica che la pianificazione di pod sia disabilitata per il tuo nodo di lavoro.
   ```
   oc get nodes
   ```
   {: pre}
   Il tuo nodo di lavoro è disabilitato per la pianificazione di pod se lo stato visualizza **SchedulingDisabled**.
 4. Forza la rimozione dei pod dal tuo nodo di lavoro e la loro ripianificazione sui nodi di lavoro rimanenti nel cluster.
    ```
    oc drain <worker_name>
    ```
    {: pre}
    Questo processo può richiedere qualche minuto.
 5. Ricarica il nodo di lavoro. Utilizza l'ID nodo di lavoro restituito dal comando `ibmcloud oc workers --cluster <cluster_name_or_ID>`.
    ```
    ibmcloud oc worker-reload --cluster <cluster_name_or_ID> --workers <worker_name_or_ID>
    ```
    {: pre}
 6. Attendi il termine del ricaricamento.
 7. Rendi disponibile il tuo nodo di lavoro per la pianificazione di pod. Utilizza il **nome** per il tuo nodo di lavoro restituito dal comando `oc get nodes`.
    ```
    oc uncordon <worker_name>
    ```
</br>


```
ibmcloud oc worker-reload --cluster CLUSTER --workers WORKER [WORKER] [--skip-master-healthcheck] [-f] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--worker <em>WORKER</em></code></dt>
<dd>Il nome o l'ID di uno o più nodi di lavoro. Utilizza uno spazio per elencare più nodi di lavoro. Questo valore è obbligatorio.</dd>

<dt><code>--skip-master-healthcheck</code></dt>
<dd>Ignora un controllo di integrità del tuo master prima di ricaricare o riavviare i nodi di lavoro.</dd>

<dt><code>-f</code></dt>
<dd>Utilizza questa opzione per forzare il ricaricamento di un nodo di lavoro senza richiedere l'intervento dell'utente. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-reload --cluster my_cluster --workers kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>


### `ibmcloud oc worker-rm`
{: #cs_worker_rm}

Rimuovere uno o più nodi di lavoro da un cluster. Se rimuovi un nodo di lavoro, il tuo cluster perde il bilanciamento. Puoi bilanciare automaticamente di nuovo il tuo pool di nodi di lavoro eseguendo il [comando](#cs_rebalance) `ibmcloud oc worker-pool-rebalance`.
{: shortdesc}



Prima di rimuovere il tuo nodo di lavoro, assicurati che i pod vengano ripianificati su altri nodi di lavoro per evitare un periodo di inattività per la tua applicazione o il danneggiamento dei dati sul nodo di lavoro.
{: tip}

1. Elenca tutti i nodi di lavoro presenti nel tuo cluster e prendi nota del **nome** del nodo di lavoro che vuoi rimuovere.
   ```
   oc get nodes
   ```
   {: pre}
   Il **nome** che viene restituito in questo comando è l'indirizzo IP privato che è assegnato al tuo nodo di lavoro. Puoi trovare ulteriori informazioni sul tuo nodo di lavoro eseguendo il comando `ibmcloud oc workers --cluster <cluster_name_or_ID>` e cercando il nodo di lavoro con lo stesso indirizzo **IP privato**.
2. Contrassegna il nodo di lavoro come non pianificabile in un processo noto come delimitazione. Quando delimiti un nodo di lavoro, lo rendi non disponibile per una futura pianificazione di pod. Utilizza il **nome** del nodo di lavoro che hai richiamato nel passo precedente.
   ```
   oc cordon <worker_name>
   ```
   {: pre}

3. Verifica che la pianificazione di pod sia disabilitata per il tuo nodo di lavoro.
   ```
   oc get nodes
   ```
   {: pre}
   Il tuo nodo di lavoro è disabilitato per la pianificazione di pod se lo stato visualizza **SchedulingDisabled**.
4. Forza la rimozione dei pod dal tuo nodo di lavoro e la loro ripianificazione sui nodi di lavoro rimanenti nel cluster.
   ```
   oc drain <worker_name>
   ```
   {: pre}
   Questo processo può richiedere qualche minuto.
5. Rimuovi il nodo di lavoro. Utilizza l'ID nodo di lavoro restituito dal comando `ibmcloud oc workers --cluster <cluster_name_or_ID>`.
   ```
   ibmcloud oc worker-rm --cluster <cluster_name_or_ID> --worker <worker_name_or_ID>
   ```
   {: pre}
6. Verifica che il nodo di lavoro venga rimosso.
   ```
   ibmcloud oc workers --cluster <cluster_name_or_ID>
   ```
   {: pre}
</br>

```
ibmcloud oc worker-rm [-f] --cluster CLUSTER --workers WORKER[,WORKER] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>-f</code></dt>
<dd>Utilizza questa opzione per forzare la rimozione di un nodo di lavoro senza richiedere l'intervento dell'utente. Questo valore è facoltativo.</dd>

<dt><code>--workers <em>WORKER</em></code></dt>
<dd>Il nome o l'ID di uno o più nodi di lavoro. Utilizza uno spazio per elencare più nodi di lavoro. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-rm --cluster my_cluster --workers kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>
### `ibmcloud oc worker-update`
{: #cs_worker_update}

Aggiorna i nodi di lavoro per applicare gli aggiornamenti e le patch di sicurezza più recenti al sistema operativo e per aggiornare la versione di Kubernetes in modo che corrisponda alla versione del master Kubernetes. Puoi aggiornare la versione di Kubernetes master con il [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_update) `ibmcloud oc cluster-update`.L'indirizzo IP del nodo di lavoro rimane lo stesso dopo l'operazione di aggiornamento.
{: shortdesc}



L'esecuzione di `ibmcloud oc worker-update` può causare tempi di inattività per le applicazioni e i tuoi servizi. Durante l'aggiornamento, tutti i pod vengono ripianificati su altri nodi di lavoro, viene ricreata l'immagine del nodo di lavoro e i dati vengono eliminati se non archiviati al di fuori del pod. Per evitare il tempo di inattività, [assicurati di avere abbastanza nodi di lavoro per gestire il carico di lavoro mentre vengono aggiornati i nodi di lavoro selezionati](/docs/containers?topic=containers-update#worker_node).
{: important}

Potresti dover modificare i tuoi file YAML per le distribuzioni prima di eseguire l'aggiornamento. Controlla questa [nota sulla release](/docs/containers?topic=containers-cs_versions) per i dettagli.

```
ibmcloud oc worker-update [-f] --cluster CLUSTER --workers WORKER[,WORKER] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster in cui elenchi i nodi di lavoro disponibili. Questo valore è obbligatorio.</dd>

<dt><code>-f</code></dt>
<dd>Utilizza questa opzione per forzare l'aggiornamento del master senza richiedere l'intervento dell'utente. Questo valore è facoltativo.</dd>

<dt><code>--workers <em>WORKER</em></code></dt>
<dd>L'ID di uno o più nodi di lavoro. Utilizza uno spazio per elencare più nodi di lavoro. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-update --cluster my_cluster --worker kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>
### `ibmcloud oc workers`
{: #cs_workers}

Elenca tutti i nodi di lavoro in un cluster.
{: shortdesc}



```
ibmcloud oc workers --cluster CLUSTER [--worker-pool POOL] [--show-pools] [--show-deleted] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster dei nodi di lavoro disponibili. Questo valore è obbligatorio.</dd>

<dt><code>--worker-pool <em>POOL</em></code></dt>
<dd>Visualizza solo i nodi di lavoro che appartengono al pool di nodi di lavoro. Per elencare i pool di nodi di lavoro disponibili, esegui `ibmcloud oc worker-pools --cluster <cluster_name_or_ID>`. Questo valore è facoltativo.</dd>

<dt><code>--show-pools</code></dt>
<dd>Elenca il pool di nodi di lavoro a cui appartiene ciascun nodo di lavoro. Questo valore è facoltativo.</dd>

<dt><code>--show-deleted</code></dt>
<dd>Visualizza i nodi di lavoro che sono stati eliminati dal cluster, incluso il motivo dell'eliminazione. Questo valore è facoltativo.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc workers --cluster my_cluster
```
{: pre}

<br />


## Comandi pool di nodi di lavoro
{: #worker-pool}

Utilizza questo gruppo di comandi per visualizzare e modificare i pool di nodi di lavoro per un cluster.
{: shortdesc}

### `ibmcloud oc worker-pool-create`
{: #cs_worker_pool_create}

Puoi creare un pool di nodi di lavoro nel tuo cluster. Quando aggiungi un pool di nodi di lavoro, per impostazione predefinita, non viene assegnata una zona. Specifica il numero di nodi di lavoro che desideri in ciascuna zona e i profili per i nodi di lavoro. Al pool di nodi di lavoro vengono fornite le versioni Kubernetes predefinite. Per terminare la creazione dei nodi di lavoro, [aggiungi una zona o le zone](#cs_zone_add) al tuo pool.
{: shortdesc}



```
ibmcloud oc worker-pool-create --name POOL_NAME --cluster CLUSTER --machine-type MACHINE_TYPE --size-per-zone WORKERS_PER_ZONE --hardware ISOLATION [--labels LABELS] [--disable-disk-encrypt] [-s] [--json]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--name <em>POOL_NAME</em></code></dt>
<dd>Il nome che desideri utilizzare per il tuo pool di nodi di lavoro.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--machine-type <em>MACHINE_TYPE</em></code></dt>
<dd>Scegli un tipo di macchina, o profilo. Puoi distribuire i tuoi nodi di lavoro come macchine virtuali su hardware condiviso o dedicato o come macchine fisiche su bare metal. I tipi di macchine fisiche e virtuali disponibili variano in base alla zona in cui distribuisci il cluster. Per ulteriori informazioni, vedi la documentazione per il [comando](#cs_machine_types) `ibmcloud oc flavors (macine-types)`. Questo valore è obbligatorio per i cluster standard e non è disponibile per i cluster gratuiti.</dd>

<dt><code>--size-per-zone <em>WORKERS_PER_ZONE</em></code></dt>
<dd>Il numero di nodi di lavoro da creare in ogni zona. Questo valore è obbligatorio e deve essere pari a 1 o superiore.</dd>

<dt><code>--hardware <em>ISOLATION</em></code></dt>
<dd>Il livello di isolamento hardware per il nodo di lavoro. Utilizza `dedicated` se vuoi avere risorse fisiche dedicate disponibili solo per te oppure `shared` per consentire la condivisione delle risorse fisiche con altri clienti IBM. L'impostazione predefinita è
`shared`. Per i profili bare metal, specifica `dedicated`. Questo valore è obbligatorio.</dd>

<dt><code>--labels <em>LABELS</em></code></dt>
<dd>Le etichette che vuoi assegnare ai nodi di lavoro nel tuo pool. Esempio: `<key1>=<val1>`,`<key2>=<val2>`</dd>

<dt><code>--disable-disk-encrpyt</code></dt>
<dd>Specifica che il disco non è crittografato. Il valore predefinito è <code>false</code>.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-pool-create --name my_pool --cluster my_cluster --machine-type b3c.4x16 --size-per-zone 6
```
{: pre}

</br>


### `ibmcloud oc worker-pool-get`
{: #cs_worker_pool_get}

Visualizza i dettagli di un pool di nodi di lavoro.
{: shortdesc}



```
ibmcloud oc worker-pool-get --worker-pool WORKER_POOL --cluster CLUSTER [-s] [--json]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--worker-pool <em>WORKER_POOL</em></code></dt>
<dd>Il nome del pool del nodo di lavoro di cui vuoi visualizzare i dettagli. Per elencare i pool di nodi di lavoro disponibili, esegui `ibmcloud oc worker-pools --cluster <cluster_name_or_ID>`. Questo valore è obbligatorio.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster in cui si trova il pool di nodi di lavoro. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-pool-get --worker-pool pool1 --cluster my_cluster
```
{: pre}

**Output di esempio**:

  ```
  Name:               pool
  ID:                 a1a11b2222222bb3c33c3d4d44d555e5-f6f777g
  State:              active
  Hardware:           shared
  Zones:              dal10,dal12
  Workers per zone:   3
  Machine type:       b3c.4x16.encrypted
  Labels:             -
  Version:            1.13.8_1512
  ```
  {: screen}

</br>
### `ibmcloud oc worker-pool-rebalance`
{: #cs_rebalance}

Ribilancia un pool di nodi di lavoro in un cluster dopo che hai eliminato un nodo di lavoro. Quando esegui questo comando, vengono aggiunti uno o più nuovi nodi di lavoro al tuo pool di nodi di lavoro in modo che il pool di nodi di lavoro abbia lo stesso numero di nodi per ogni zona che tu hai specificato.
{: shortdesc}



```
ibmcloud oc worker-pool-rebalance --cluster CLUSTER --worker-pool WORKER_POOL [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code><em>--cluster CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code><em>--worker-pool WORKER_POOL</em></code></dt>
<dd>Il pool di nodi di lavoro che desideri bilanciare di nuovo. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-pool-rebalance --cluster my_cluster --worker-pool my_pool
```
{: pre}

</br>
### `ibmcloud oc worker-pool-resize`
{: #cs_worker_pool_resize}

Ridimensiona il tuo pool di nodi di lavoro per aumentare o diminuire il numero di nodi di lavoro presenti in ogni zona del tuo cluster. Il tuo pool di nodi di lavoro deve avere almeno un nodo di lavoro.
{: shortdesc}



```
ibmcloud oc worker-pool-resize --worker-pool WORKER_POOL --cluster CLUSTER --size-per-zone WORKERS_PER_ZONE [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--worker-pool <em>WORKER_POOL</em></code></dt>
<dd>Il nome del pool del nodo di lavoro che vuoi aggiornare. Questo valore è obbligatorio.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster per cui vuoi ridimensionare i pool di nodi di lavoro. Questo valore è obbligatorio.</dd>

<dt><code>--size-per-zone <em>WORKERS_PER_ZONE</em></code></dt>
<dd>Il numero di nodi di lavoro che vuoi avere in ciascuna zona. Questo valore è obbligatorio e deve essere pari a 1 o superiore.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>

</dl>

**Esempio**:
```
ibmcloud oc worker-pool-resize --cluster my_cluster --worker-pool my_pool --size-per-zone 3
```
{: pre}

</br>
### `ibmcloud oc worker-pool-rm`
{: #cs_worker_pool_rm}

Rimuovi un pool di nodi di lavoro dal tuo cluster. Tutti i nodi di lavoro nel pool vengono eliminati. I tuoi pod vengono ripianificati quando esegui un'eliminazione. Per evitare tempi di inattività, assicurati di avere abbastanza nodi di lavoro per eseguire il tuo carico di lavoro.
{: shortdesc}



```
ibmcloud oc worker-pool-rm --worker-pool WORKER_POOL --cluster CLUSTER [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--worker-pool <em>WORKER_POOL</em></code></dt>
<dd>Il nome del pool del nodo di lavoro che vuoi rimuovere. Questo valore è obbligatorio.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster da cui desideri rimuovere il pool di nodi di lavoro. Questo valore è obbligatorio.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-pool-rm --cluster my_cluster --worker-pool pool1
```
{: pre}

</br>
### `ibmcloud oc worker-pools`
{: #cs_worker_pools}

Elenca tutti i pool di nodi di lavoro in un cluster.
{: shortdesc}



```
ibmcloud oc worker-pools --cluster CLUSTER [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Visualizzatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--cluster <em>CLUSTER_NAME_OR_ID</em></code></dt>
<dd>Il nome o l'ID del cluster per cui vuoi elencare i pool di nodi di lavoro. Questo valore è obbligatorio.</dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc worker-pools --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc zone-add`
{: #cs_zone_add}

Dopo che hai creato un cluster o un pool di nodi di lavoro, puoi aggiungere una zona. Quando aggiungi una zona, i nodi di lavoro vengono aggiunti alla nuova zona in modo da corrispondere al numero di nodi di lavoro per zona che hai specificato per il pool di nodi di lavoro. Puoi aggiungere più di una zona solo se il tuo cluster si trova in una ubicazione metropolitana multizona.
{: shortdesc}



```
ibmcloud oc zone-add --zone ZONE --cluster CLUSTER --worker-pools WORKER_POOL1[,WORKER_POOL2] --private-vlan PRIVATE_VLAN [--public-vlan PUBLIC_VLAN] [--private-only] [--json] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>La zona che desideri aggiungere. Deve essere una [zona che supporta il multizona](/docs/containers?topic=containers-regions-and-zones#zones) all'interno della regione del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--worker-pool <em>WORKER_POOLS</em></code></dt>
<dd>Un elenco separato da virgole dei pool di nodi di lavoro a cui viene aggiunta la zona. È necessario almeno un pool di nodi di lavoro.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd><p>L'ID della VLAN privata. Questo valore è condizionato.</p>
    <p>Se hai una VLAN privata nella zona, questo valore deve corrispondere all'ID VLAN privata di uno o più nodi di lavoro nel cluster. Per vedere le VLAN disponibili, esegui <code>ibmcloud oc cluster-get --cluster &lt;cluster&gt; --showResources</code>. I nuovi nodi di lavoro vengono aggiunti alla VLAN che hai specificato, ma le VLAN per i nodi di lavoro esistenti non vengono modificate.</p>
    <p>Se non hai una VLAN privata o pubblica in tale zona, non specificare questa opzione. Vengono create automaticamente per te una VLAN privata e una pubblica quando aggiungi inizialmente una zona al tuo pool di nodi di lavoro.</p>
    <p>Se hai più VLAN per un cluster, più sottoreti sulla stessa VLAN o un cluster multizona, devi abilitare una [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) per il tuo account dell'infrastruttura IBM Cloud in modo che i tuoi nodi di lavoro possano comunicare tra loro sulla rete privata. Per abilitare VRF, [contatta il tuo rappresentante dell'account dell'infrastruttura IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Per controllare se una VRF è già abilitata, utilizza il comando `ibmcloud account show`. Se non puoi o non vuoi abilitare VRF, abilita lo [spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Per eseguire questa azione, ti serve l'[autorizzazione dell'infrastruttura](/docs/containers?topic=containers-users#infra_access) **Rete > Gestisci il VLAN Spanning di rete** oppure puoi richiedere al proprietario dell'account di abilitarlo. Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando `ibmcloud oc vlan-spanning-get --region <region>`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get).</p></dd>

<dt><code>--public-vlan <em>PUBLIC_VLAN</em></code></dt>
<dd><p>L'ID della VLAN pubblica. Questo valore è obbligatorio se desideri esporre i carichi di lavoro sui nodi al pubblico una volta che hai creato il cluster. Deve corrispondere all'ID VLAN pubblica di uno o più nodi di lavoro nel cluster per la zona. Per vedere le VLAN disponibili, esegui <code>ibmcloud oc cluster-get --cluster &lt;cluster&gt; --showResources</code>. I nuovi nodi di lavoro vengono aggiunti alla VLAN che hai specificato, ma le VLAN per i nodi di lavoro esistenti non vengono modificate.</p>
    <p>Se non hai una VLAN privata o pubblica in tale zona, non specificare questa opzione. Vengono create automaticamente per te una VLAN privata e una pubblica quando aggiungi inizialmente una zona al tuo pool di nodi di lavoro.</p>
    <p>Se hai più VLAN per un cluster, più sottoreti sulla stessa VLAN o un cluster multizona, devi abilitare una [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) per il tuo account dell'infrastruttura IBM Cloud in modo che i tuoi nodi di lavoro possano comunicare tra loro sulla rete privata. Per abilitare VRF, [contatta il tuo rappresentante dell'account dell'infrastruttura IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Per controllare se una VRF è già abilitata, utilizza il comando `ibmcloud account show`. Se non puoi o non vuoi abilitare VRF, abilita lo [spanning della VLAN](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Per eseguire questa azione, ti serve l'[autorizzazione dell'infrastruttura](/docs/containers?topic=containers-users#infra_access) **Rete > Gestisci il VLAN Spanning di rete** oppure puoi richiedere al proprietario dell'account di abilitarlo. Per controllare se lo spanning della VLAN è già abilitato, utilizza il [comando `ibmcloud oc vlan-spanning-get --region <region>`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get).</p></dd>

<dt><code>--private-only </code></dt>
<dd>Utilizza questa opzione per impedire la creazione di una VLAN pubblica. Obbligatoria solo quando specifichi l'indicatore `--private-vlan` e non includi l'indicatore `--public-vlan`.<p class="note">Se i nodi di lavoro sono configurati solo con una VLAN privata, devi abilitare l'endpoint del servizio privato o configurare un dispositivo gateway. Per ulteriori informazioni, vedi [Pianificazione della configurazione dei tuoi nodi di lavoro e cluster privati](/docs/containers?topic=containers-plan_clusters#private_clusters).</p></dd>

<dt><code>--json</code></dt>
<dd>Stampa l'output del comando in formato JSON. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc zone-add --zone dal10 --cluster my_cluster --worker-pools pool1,pool2,pool3 --private-vlan 2294021
```
{: pre}

</br>


### `ibmcloud oc zone-network-set`
{: #cs_zone_network_set}

**Solo cluster multizona**: imposta i metadati di rete per un pool di nodi di lavoro per utilizzare una VLAN pubblica o privata diversa per la zona rispetto a quella utilizzata in precedenza. I nodi di lavoro che sono stati già creati nel pool continuano ad utilizzare la VLAN pubblica o privata precedente, ma i nuovi nodi di lavoro nel pool utilizzeranno i nuovi dati di rete.
{: shortdesc}



```
ibmcloud oc zone-network-set --zone ZONE --cluster CLUSTER --worker-pools WORKER_POOL1[,WORKER_POOL2] --private-vlan PRIVATE_VLAN [--public-vlan PUBLIC_VLAN] [--private-only] [-f] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>La zona che desideri aggiungere. Deve essere una [zona che supporta il multizona](/docs/containers?topic=containers-regions-and-zones#zones) all'interno della regione del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>--worker-pool <em>WORKER_POOLS</em></code></dt>
<dd>Un elenco separato da virgole dei pool di nodi di lavoro a cui viene aggiunta la zona. È necessario almeno un pool di nodi di lavoro.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>L'ID della VLAN privata. Questo valore è obbligatorio, indipendentemente dal fatto che tu voglia utilizzare lo stesso VLAN privato oppure uno differente da quello che hai usato per gli altri tuoi nodi di lavoro. I nuovi nodi di lavoro vengono aggiunti alla VLAN che hai specificato, ma le VLAN per i nodi di lavoro esistenti non vengono modificate.<p class="note">Le VLAN private e pubbliche devono essere compatibili, cosa che puoi determinare dal prefisso ID **Router**.</p></dd>

<dt><code>--public-vlan <em>PUBLIC_VLAN</em></code></dt>
<dd>L'ID della VLAN pubblica. Questo valore è obbligatorio solo se vuoi modificare la VLAN pubblica per la zona. Per modificare la VLAN pubblica, devi sempre fornire una VLAN privata compatibile. I nuovi nodi di lavoro vengono aggiunti alla VLAN che hai specificato, ma le VLAN per i nodi di lavoro esistenti non vengono modificate.<p class="note">Le VLAN private e pubbliche devono essere compatibili, cosa che puoi determinare dal prefisso ID **Router**.</p></dd>

<dt><code>--private-only </code></dt>
<dd>Facoltativo: annulla l'impostazione della VLAN pubblica in modo che i nodi di lavoro in questa zona siano connessi solo a una VLAN privata.</dd>

<dt><code>-f</code></dt>
<dd>Forza l'esecuzione del comando senza richiedere l'intervento dell'utente. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Utilizzo**:
<ol><li>Controlla le VLAN che sono disponibili nel tuo cluster. <pre class="pre"><code>ibmcloud oc cluster get --cluster &lt;cluster_name_or_ID&gt; --showResources</code></pre><p>Output di esempio:</p>
<pre class="screen"><code>Subnet VLANs
VLAN ID   Subnet CIDR         Public   User-managed
229xxxx   169.xx.xxx.xxx/29   true     false
229xxxx   10.xxx.xx.x/29      false    false</code></pre></li>
<li>Controlla che gli ID VLAN pubblici e privati che vuoi utilizzare siano compatibili. Per essere compatibili, il <strong>Router</strong> deve avere lo stesso ID pod. I router della VLAN privata iniziano sempre con <code>bcr</code> (router back-end) e i router della VLAN pubblica iniziano sempre con <code>fcr</code> (router front-end). Quando crei un cluster e specifichi le VLAN pubbliche e private, la combinazione di numeri e lettere dopo tali prefissi devono corrispondere.<pre class="pre"><code>ibmcloud oc vlans --zone &lt;zone&gt;</code></pre><p>Output di esempio:</p>
<pre class="screen"><code>ID        Name   Number   Type      Router         Supports Virtual Workers
229xxxx          1234     private   bcr01a.dal12   true
229xxxx          5678     public    fcr01a.dal12   true</code></pre><p>Nota che gli ID pod <strong>Router</strong> corrispondono: `01a` e `01a`. Se un ID di pod era `01a` e l'altro era `02a`, non è possibile impostare questi ID VLAN pubblici e privati per il tuo pool di nodi di lavoro.</p></li>
<li>Se non hai alcuna VLAN disponibile, puoi <a href="/docs/infrastructure/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans">ordinare delle nuove VLAN</a>.</li></ol>

**Esempio**:
```
ibmcloud oc zone-network-set --zone dal10 --cluster my_cluster --worker-pools pool1,pool2,pool3 --private-vlan 2294021
```
{: pre}

</br>
### `ibmcloud oc zone-rm`
{: #cs_zone_rm}

**Solo cluster multizona**: rimuovi una zona da tutti i pool di nodi di lavoro nel tuo cluster. Tutti i nodi di lavoro nel pool di nodi di lavoro per questa zona vengono eliminati.
{: shortdesc}



Prima di rimuovere una zona, assicurati di disporre di un numero sufficiente di nodi di lavoro in altre zone nel cluster in modo da consentire la ripianificazione dei tuoi pod. La ripianificazione dei pod può evitare un tempo di inattività per la tua applicazione o un danneggiamento dei dati sul tuo nodo di lavoro.
{: tip}

```
ibmcloud oc zone-rm --zone ZONE --cluster CLUSTER [-f] [-s]
```
{: pre}

**Autorizzazioni minime richieste**: ruolo della piattaforma **Operatore** per il cluster in {{site.data.keyword.containerlong_notm}}

**Opzioni comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>La zona che vuoi rimuovere. Questo valore è obbligatorio.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Il nome o l'ID del cluster. Questo valore è obbligatorio.</dd>

<dt><code>-f</code></dt>
<dd>Forza l'aggiornamento senza richiedere l'intervento dell'utente. Questo valore è facoltativo.</dd>

<dt><code>-s</code></dt>
<dd>Non visualizza il messaggio dei promemoria di aggiornamento o del giorno. Questo valore è facoltativo.</dd>
</dl>

**Esempio**:
```
ibmcloud oc zone-rm --zone dal10 --cluster my_cluster
```
{: pre}


