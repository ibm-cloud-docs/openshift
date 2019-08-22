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

# Apertura delle porte e degli indirizzi IP necessari nel tuo firewall
{: #firewall}

Riesamina le seguenti situazioni in cui potresti aver bisogno di aprire porte e indirizzi IP specifici nei tuoi firewall per i tuoi cluster {{site.data.keyword.openshiftlong}}.
{:shortdesc}

* [Per eseguire i comandi `ibmcloud` e `ibmcloud oc`](#firewall_bx) dal tuo sistema locale quando le politiche di rete aziendali impediscono l'accesso agli endpoint di rete pubblici tramite proxy o firewall.
* [Per eseguire i comandi `oc`](#firewall_kubectl) dal tuo sistema locale quando le politiche di rete aziendali impediscono l'accesso agli endpoint di rete pubblici tramite proxy o firewall.
* [Per eseguire i comandi `calicoctl`](#firewall_calicoctl) dal tuo sistema locale quando le politiche di rete aziendali impediscono l'accesso agli endpoint di rete pubblici tramite proxy o firewall.
* [Per consentire le comunicazioni tra il master e i nodi di lavoro](#firewall_outbound) quando è configurato un firewall per i nodi di lavoro o le impostazioni del firewall sono personalizzate nel tuo account dell'infrastruttura IBM Cloud.
* [Per consentire al cluster di accedere alle risorse su un firewall sulla rete privata](#firewall_private).
* [Per consentire al cluster di accedere alle risorse quando le politiche di rete Calico bloccano l'uscita del nodo di lavoro pubblico o privato](#firewall_calico_egress).
* [Per accedere al servizio NodePort, al servizio del programma di bilanciamento del carico o a Ingress dall'esterno del cluster](#firewall_inbound).
* [Per consentire al cluster di accedere a servizi eseguiti all'interno o all'esterno di {{site.data.keyword.cloud_notm}} o in loco e che sono protetti da un firewall](#whitelist_workers).

<br />


## Esecuzione dei comandi `ibmcloud` e `ibmcloud oc` da dietro un firewall
{: #firewall_bx}

Se le politiche di rete aziendali impediscono l'accesso dal tuo sistema locale agli endpoint pubblici tramite i proxy o i firewall, per eseguire i comandi `ibmcloud` e `ibmcloud oc`, devi consentire l'accesso TCP per {{site.data.keyword.cloud_notm}} e Red Hat OpenShift on IBM Cloud.
{:shortdesc}

1. Consenti l'accesso a `cloud.ibm.com` sulla porta 443 nel tuo firewall.
2. Verifica la tua connessione accedendo a {{site.data.keyword.cloud_notm}} tramite questo endpoint API.
  ```
  ibmcloud login -a https://cloud.ibm.com/
  ```
  {: pre}
3. Consenti l'accesso a `containers.cloud.ibm.com` sulla porta 443 nel tuo firewall.
4. Verifica la tua connessione. Se l'accesso è configurato, vengono visualizzate delle barche nell'output.
   ```
   curl https://containers.cloud.ibm.com/v1/
   ```
   {: pre}

   Output di esempio:
   ```
                                     )___(
                              _______/__/_
                     ___     /===========|   ___
    ____       __   [\\\]___/____________|__[///]   __
    \   \_____[\\]__/___________________________\__[//]___
     \                                                    |
      \                                                  /
   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

   ```
   {: screen}

<br />


## Esecuzione dei comandi `oc` da dietro un firewall
{: #firewall_kubectl}

Se le politiche di rete aziendali impediscono l'accesso dal tuo sistema locale agli endpoint pubblici tramite i proxy o i firewall, per eseguire i comandi `oc`, devi consentire l'accesso TCP per il cluster.
{:shortdesc}

Quando si crea un cluster, la porta negli URL degli endpoint del servizio viene assegnata in modo casuale con un valore compreso nell'intervallo 20000-32767. Puoi scegliere di aprire l'intervallo di porte 20000-32767 per tutti i cluster che possono essere creati oppure scegliere di consentire l'accesso a un cluster esistente specifico.

Prima di cominciare, consenti l'accesso a [eseguire i comandi `ibmcloud oc`](#firewall_bx).

Per concedere l'accesso per un cluster specifico:

1. Accedi alla CLI {{site.data.keyword.cloud_notm}}. Immetti le tue credenziali
{{site.data.keyword.cloud_notm}} quando richiesto. Se hai un account federato, includi l'opzione `--sso`.

   ```
   ibmcloud login [--sso]
   ```
   {: pre}

2. Se il cluster si trova in un gruppo di risorse diverso da quello di `default`, specifica tale gruppo di risorse. Per visualizzare il gruppo di risorse a cui appartiene ciascun cluster, esegui `ibmcloud oc clusters`.**Nota**: devi disporre almeno del [ruolo **Visualizzatore**](/docs/containers?topic=containers-users#platform) per il gruppo di risorse.
   ```
   ibmcloud target -g <resource_group_name>
   ```
   {: pre}

4. Richiama il nome del tuo cluster.

   ```
   ibmcloud oc clusters
   ```
   {: pre}

5. Richiama gli URL degli endpoint del servizio per il tuo cluster.
 * Se viene popolato solo il campo **Public Service Endpoint URL**, ottieni questo URL. I tuoi utenti del cluster autorizzati possono accedere al master tramite questo endpoint sulla rete pubblica.
 * Se viene popolato solo il campo **Private Service Endpoint URL**, ottieni questo URL. I tuoi utenti del cluster autorizzati possono accedere al master tramite questo endpoint sulla rete privata.
 * Se vengono popolati entrambi i campi **Public Service Endpoint URL** e **Private Service Endpoint URL**, ottieni i due URL. I tuoi utenti del cluster autorizzati possono accedere al master tramite l'endpoint pubblico sulla rete pubblica o l'endpoint privato sulla rete privata.

  ```
  ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Output di esempio:
  ```
  ...
  Public Service Endpoint URL:    https://c3.<region>.containers.cloud.ibm.com:30426
  Private Service Endpoint URL:   https://c3-private.<region>.containers.cloud.ibm.com:31140
  ...
  ```
  {: screen}

6. Consenti l'accesso agli URL e alle porte degli endpoint del servizio che hai ottenuto nel passo precedente. Se il tuo firewall è basato su IP, puoi vedere quali indirizzi IP vengono aperti quando consenti l'accesso agli URL degli endpoint del servizio controllando [questa tabella](#master_ips).

7. Verifica la tua connessione.
  * Se è abilitato l'endpoint del servizio pubblico:
    ```
    curl --insecure <public_service_endpoint_URL>/version
    ```
    {: pre}

    Comando di esempio:
    ```
    curl --insecure https://c3.<region>.containers.cloud.ibm.com:31142/version
    ```
    {: pre}

    Output di esempio:
    ```
    {
     "major": "1",
     "minor": "7+",
     "gitVersion": "v1.7.4-2+eb9172c211dc41",
     "gitCommit": "eb9172c211dc4108341c0fd5340ee5200f0ec534",
     "gitTreeState": "clean",
     "buildDate": "2017-11-16T08:13:08Z",
     "goVersion": "go1.8.3",
     "compiler": "gc",
     "platform": "linux/amd64"
   }
    ```
    {: screen}
  * Se è abilitato l'endpoint del servizio privato, devi trovarti nella tua rete privata {{site.data.keyword.cloud_notm}} o connetterti alla rete privata attraverso una connessione VPN per verificare la tua connessione al master. **Nota**: devi [esporre l'endpoint master tramite un programma di bilanciamento del carico privato](/docs/containers?topic=containers-clusters#access_on_prem) in modo che gli utenti possano accedere al master tramite una VPN o una connessione {{site.data.keyword.BluDirectLink}}.
    ```
    curl --insecure <private_service_endpoint_URL>/version
    ```
    {: pre}

    Comando di esempio:
    ```
    curl --insecure https://c3-private.<region>.containers.cloud.ibm.com:31142/version
    ```
    {: pre}

    Output di esempio:
    ```
    {
     "major": "1",
     "minor": "7+",
     "gitVersion": "v1.7.4-2+eb9172c211dc41",
     "gitCommit": "eb9172c211dc4108341c0fd5340ee5200f0ec534",
     "gitTreeState": "clean",
     "buildDate": "2017-11-16T08:13:08Z",
     "goVersion": "go1.8.3",
     "compiler": "gc",
     "platform": "linux/amd64"
   }
    ```
    {: screen}

8. Facoltativo: ripeti questa procedura per ogni cluster che devi esporre.

<br />


## Esecuzione dei comandi `calicoctl` da dietro un firewall
{: #firewall_calicoctl}

Se le politiche di rete aziendali impediscono l'accesso dal tuo sistema locale agli endpoint pubblici tramite i proxy o i firewall, per eseguire i comandi `calicoctl`, devi consentire l'accesso TCP per i comandi Calico.
{:shortdesc}

Prima di cominciare, consenti l'accesso per eseguire i comandi [`ibmcloud`](#firewall_bx) e [`oc`](#firewall_kubectl).

1. Richiama l'indirizzo IP dall'URL master che hai utilizzato per consentire i comandi [`oc`](#firewall_kubectl).

2. Ottieni la porta per etcd.

  ```
  oc get cm -n kube-system cluster-info -o yaml | grep etcd_host
  ```
  {: pre}

3. Consenti l'accesso alle politiche Calico tramite l'indirizzo IP dell'URL master e la porta etcd.

<br />


## Concessione al cluster dell'accesso alle risorse dell'infrastruttura e ad altri servizi su un firewall pubblico
{: #firewall_outbound}

Permetti al tuo cluster di accedere ai servizi e alle risorse dell'infrastruttura da dietro un firewall pubblico, come ad esempio per le regioni Red Hat OpenShift on IBM Cloud, {{site.data.keyword.registrylong_notm}}, {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), {{site.data.keyword.monitoringlong_notm}}, {{site.data.keyword.loganalysislong_notm}}, gli IP privati dell'infrastruttura IBM Cloud e il traffico in uscita per le attestazioni del volume persistente.
{:shortdesc}

Vuoi utilizzare le politiche Calico perché fungano da tuo firewall del cluster invece di un firewall del dispositivo gateway? Vedi [Isolamento dei cluster sulla rete pubblica](/docs/containers?topic=containers-network_policies#isolate_workers_public).
{: tip}

A seconda della configurazione del tuo cluster, accedi ai servizi utilizzando gli indirizzi IP pubblici, privati o entrambi. Se hai un cluster con nodi di lavoro su VLAN pubbliche e private dietro un firewall sia per le reti pubbliche che private, devi aprire la connessione per gli indirizzi IP pubblici e privati. Se il tuo cluster ha nodi di lavoro solo sulla VLAN privata dietro un firewall, puoi aprire la connessione solo agli indirizzi IP privati.
{: note}

1.  Prendi nota dell'indirizzo IP pubblico di tutti i tuoi nodi di lavoro nel cluster.

    ```
    ibmcloud oc workers --cluster <cluster_name_or_ID>
    ```
    {: pre}

2.  Consenti il traffico di rete in uscita da <em>&lt;each_worker_node_publicIP&gt;</em> di origine alle porte TCP/UDP di destinazione comprese nell'intervallo 20000-32767 e alla porta 443, e ai seguenti indirizzi IP e gruppi di reti. Questi indirizzi IP consentono ai nodi di lavoro di comunicare con il master cluster. Se hai un firewall aziendale che impedisce alla tua macchina locale di accedere agli endpoint internet pubblici, esegui questa operazione anche per la tua macchina locale in modo da poter accedere al master cluster.

    Devi consentire il traffico in uscita alla porta 443 per tutte le zone all'interno della regione per bilanciare il carico durante il processo di avvio. Ad esempio, se il tuo cluster si trova negli Stati Uniti Sud, devi consentire il traffico dagli IP pubblici su ciascuno dei tuoi nodi di lavoro alla porta 443 dell'indirizzo IP per tutte le zone.
    {: important}

    {: #master_ips}
    <table summary="La prima riga nella tabella si estende su entrambe le colonne. Le righe rimanenti devono essere lette da sinistra a destra, con la zona server nella colonna uno e gli indirizzi IP corrispondenti nella colonna due.">
      <caption>Gli indirizzi IP da aprire per il traffico in uscita</caption>
          <thead>
          <th>Regione</th>
          <th>Zona</th>
          <th>Indirizzo IP pubblico</th>
          <th>Indirizzo IP privato</th>
          </thead>
        <tbody>
          <tr>
            <td>Asia Pacifico Nord</td>
            <td>che01<br>hkg02<br>seo01<br>sng01<br><br>tok02, tok04, tok05</td>
            <td><code>169.38.70.10</code><br><code>169.56.132.234</code><br><code>169.56.69.242</code><br><code>161.202.186.226</code><br><br><code>161.202.126.210, 128.168.71.117, 165.192.69.69</code></td>
            <td><code>166.9.40.7</code><br><code>166.9.42.7</code><br><code>166.9.44.5</code><br><code>166.9.40.8</code><br><br><code>166.9.40.6, 166.9.42.6, 166.9.44.4</code></td>
           </tr>
          <tr>
             <td>Asia Pacifico Sud</td>
             <td>mel01<br><br>syd01, syd04, syd05</td>
             <td><code>168.1.97.67</code><br><br><code>168.1.8.195, 130.198.66.26, 168.1.12.98, 130.198.64.19</code></td>
             <td><code>166.9.54.10</code><br><br><code>166.9.52.14, 166.9.52.15, 166.9.54.11, 166.9.54.13, 166.9.54.12</code></td>
          </tr>
          <tr>
             <td>Europa Centrale</td>
             <td>ams03<br>mil01<br>osl01<br>par01<br><br>fra02, fra04, fra05</td>
             <td><code>169.50.169.110, 169.50.154.194</code><br><code>159.122.190.98, 159.122.141.69</code><br><code>169.51.73.50</code><br><code>159.8.86.149, 159.8.98.170</code><br><br><code>169.50.56.174, 161.156.65.42, 149.81.78.114</code></td>
             <td><code>166.9.28.17, 166.9.30.11</code><br><code>166.9.28.20, 166.9.30.12</code><br><code>166.9.32.8</code><br><code>166.9.28.19, 166.9.28.22</code><br><br><code>	166.9.28.23, 166.9.30.13, 166.9.32.9</code></td>
            </tr>
          <tr>
            <td>Regno Unito Sud</td>
            <td>lon02, lon04, lon05, lon06</td>
            <td><code>159.122.242.78, 158.175.111.42, 158.176.94.26, 159.122.224.242, 158.175.65.170, 158.176.95.146</code></td>
            <td><code>166.9.34.5, 166.9.34.6, 166.9.36.10, 166.9.36.11, 166.9.36.12, 166.9.36.13, 166.9.38.6, 166.9.38.7</code></td>
          </tr>
          <tr>
            <td>Stati Uniti Est</td>
             <td>mon01<br>tor01<br><br>wdc04, wdc06, wdc07</td>
             <td><code>169.54.126.219</code><br><code>169.53.167.50</code><br><br><code>169.63.88.186, 169.60.73.142, 169.61.109.34, 169.63.88.178, 169.60.101.42, 169.61.83.62</code></td>
             <td><code>166.9.20.11</code><br><code>166.9.22.8</code><br><br><code>166.9.20.12, 166.9.20.13, 166.9.22.9, 166.9.22.10, 166.9.24.4, 166.9.24.5</code></td>
          </tr>
          <tr>
            <td>Stati Uniti Sud</td>
            <td>hou02<br>mex01<br>sao01<br>sjc03<br>sjc04<br><br>dal10,dal12,dal13</td>
            <td><code>184.173.44.62</code><br><code>169.57.100.18</code><br><code>169.57.151.10</code><br><code>169.45.67.210</code><br><code>169.62.82.197</code><br><br><code>169.46.7.238, 169.48.230.146, 169.61.29.194, 169.46.110.218, 169.47.70.10, 169.62.166.98, 169.48.143.218, 169.61.177.2, 169.60.128.2</code></td>
            <td><code>166.9.15.74</code><br><code>166.9.15.76</code><br><code>166.9.12.143</code><br><code>166.9.12.144</code><br><code>166.9.15.75</code><br><br><code>166.9.12.140, 166.9.12.141, 166.9.12.142, 166.9.15.69, 166.9.15.70, 166.9.15.72, 166.9.15.71, 166.9.15.73, 166.9.16.183, 166.9.16.184, 166.9.16.185</code></td>
          </tr>
          </tbody>
        </table>

3.  {: #firewall_registry}Per permettere ai nodi di lavoro di comunicare con {{site.data.keyword.registrylong_notm}}, consenti il traffico di rete in uscita dai nodi di lavoro alle [regioni {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_overview#registry_regions):
  - `TCP port 443, port 4443 FROM <each_worker_node_publicIP> TO <registry_subnet>`
  -  Sostituisci <em>&lt;registry_subnet&gt;</em> con la sottorete del registro per cui desideri consentire il traffico. Il registro globale archivia le immagini pubbliche fornite da IBM e i registri regionali archiviano le tue proprie immagini pubbliche e private. La porta 4443 è richiesta per funzioni notarili, come ad esempio la [Verifica delle firme delle immagini](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent). <table summary="La prima riga nella tabella si estende su entrambe le colonne. Le righe rimanenti devono essere lette da sinistra a destra, con la zona server nella colonna uno e gli indirizzi IP corrispondenti nella colonna due.">
  <caption>Gli indirizzi IP da aprire per il traffico del registro</caption>
    <thead>
      <th>Regione Red Hat OpenShift on IBM Cloud</th>
      <th>Indirizzo del registro</th>
      <th>Sottoreti pubbliche del registro</th>
      <th>Indirizzi IP privati del registro</th>
    </thead>
    <tbody>
      <tr>
        <td>Registro globale tra le regioni <br>Regioni Red Hat OpenShift on IBM Cloud</td>
        <td><code>icr.io</code><br><br>
        Obsoleto: <code>registry.bluemix.net</code></td>
        <td><code>169.60.72.144/28</code></br><code>169.61.76.176/28</code></br><code>169.62.37.240/29</code></br><code>169.60.98.80/29</code></br><code>169.63.104.232/29</code></td>
        <td><code>166.9.20.4</code></br><code>166.9.22.3</code></br><code>166.9.24.2</code></td>
      </tr>
      <tr>
        <td>Asia Pacifico Nord</td>
        <td><code>jp.icr.io</code><br><br>
        Obsoleto: <code>registry.au-syd.bluemix.net</code></td>
        <td><code>161.202.146.86/29</code></br><code>128.168.71.70/29</code></br><code>165.192.71.222/29</code></td>
        <td><code>166.9.40.3</code></br><code>166.9.42.3</code></br><code>166.9.44.3</code></td>
      </tr>
      <tr>
        <td>Asia Pacifico Sud</td>
        <td><code>au.icr.io</code><br><br>
        Obsoleto: <code>registry.au-syd.bluemix.net</code></td>
        <td><code>168.1.45.160/27</code></br><code>168.1.139.32/27</code></br><code>168.1.1.240/29</code></br><code>130.198.88.128/29</code></br><code>135.90.66.48/29</code></td>
        <td><code>166.9.52.2</code></br><code>166.9.54.2</code></br><code>166.9.56.3</code></td>
      </tr>
      <tr>
        <td>Europa Centrale</td>
        <td><code>de.icr.io</code><br><br>
        Obsoleto: <code>registry.eu-de.bluemix.net</code></td>
        <td><code>169.50.56.144/28</code></br><code>159.8.73.80/28</code></br><code>169.50.58.104/29</code></br><code>161.156.93.16/29</code></br><code>149.81.79.152/29</code></td>
        <td><code>166.9.28.12</code></br><code>166.9.30.9</code></br><code>166.9.32.5</code></td>
       </tr>
       <tr>
        <td>Regno Unito Sud</td>
        <td><code>uk.icr.io</code><br><br>
        Obsoleto: <code>registry.eu-gb.bluemix.net</code></td>
        <td><code>159.8.188.160/27</code></br><code>169.50.153.64/27</code></br><code>158.175.97.184/29</code></br><code>158.176.105.64/29</code></br><code>141.125.71.136/29</code></td>
        <td><code>166.9.36.9</code></br><code>166.9.38.5</code></br><code>166.9.34.4</code></td>
       </tr>
       <tr>
        <td>Stati Uniti Est, Stati Uniti Sud</td>
        <td><code>us.icr.io</code><br><br>
        Obsoleto: <code>registry.ng.bluemix.net</code></td>
        <td><code>169.55.39.112/28</code></br><code>169.46.9.0/27</code></br><code>169.55.211.0/27</code></br><code>169.61.234.224/29</code></br><code>169.61.135.160/29</code></br><code>169.61.46.80/29</code></td>
        <td><code>166.9.12.114</code></br><code>166.9.15.50</code></br><code>166.9.16.173</code></td>
       </tr>
      </tbody>
    </table>

4. Consenti il traffico di rete in uscita dal tuo nodo di lavoro a {{site.data.keyword.cloud_notm}} IAM (Identity and Access Management). Il tuo firewall deve essere di livello 7 per inserire in whitelist il nome dominio IAM. IAM non ha specifici indirizzi IP che puoi inserire in whitelist. Se il tuo firewall non supporta il livello 7, puoi consentire tutto il traffico di rete HTTPS sulla porta 443.
    - `TCP port 443 FROM <each_worker_node_publicIP> TO https://iam.bluemix.net`
    - `TCP port 443 FROM <each_worker_node_publicIP> TO https://iam.cloud.ibm.com`

5. Facoltativo: consenti il traffico di rete in uscita dai nodi di lavoro ai servizi {{site.data.keyword.monitoringlong_notm}}, {{site.data.keyword.loganalysislong_notm}}, Sysdig e LogDNA:
    *   **{{site.data.keyword.monitoringlong_notm}}**:
        <pre class="screen">TCP port 443, port 9095 FROM &lt;each_worker_node_public_IP&gt; TO &lt;monitoring_subnet&gt;</pre>
        Sostituisci <em>&lt;monitoring_subnet&gt;</em> con le sottoreti per le regioni di monitoraggio per cui desideri consentire il traffico:
        <p><table summary="La prima riga nella tabella si estende su entrambe le colonne. Le righe rimanenti devono essere lette da sinistra a destra, con la zona server nella colonna uno e gli indirizzi IP corrispondenti nella colonna due.">
          <caption>Gli indirizzi IP da aprire per il traffico di monitoraggio</caption>
                <thead>
                <th>Regione {{site.data.keyword.containerlong_notm}}</th>
                <th>Indirizzo di monitoraggio</th>
                <th>Sottoreti di monitoraggio</th>
                </thead>
              <tbody>
                <tr>
                 <td>Europa Centrale</td>
                 <td><code>metrics.eu-de.bluemix.net</code></td>
                 <td><code>158.177.65.80/30</code></td>
                </tr>
                <tr>
                 <td>Regno Unito Sud</td>
                 <td><code>metrics.eu-gb.bluemix.net</code></td>
                 <td><code>169.50.196.136/29</code></td>
                </tr>
                <tr>
                  <td>Stati Uniti Est, Stati Uniti Sud, Asia Pacifico Nord, Asia Pacifico Sud</td>
                  <td><code>metrics.ng.bluemix.net</code></td>
                  <td><code>169.47.204.128/29</code></td>
                 </tr>
                </tbody>
              </table></p>
    *   **{{site.data.keyword.mon_full_notm}}**:
        <pre class="screen">TCP port 443, port 6443 FROM &lt;each_worker_node_public_IP&gt; TO &lt;sysdig_public_IP&gt;</pre>
        Sostituisci `<sysdig_public_IP>` con gli [indirizzi IP Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network).
    *   **{{site.data.keyword.loganalysislong_notm}}**:
        <pre class="screen">TCP port 443, port 9091 FROM &lt;each_worker_node_public_IP&gt; TO &lt;logging_public_IP&gt;</pre>
        Sostituisci <em>&lt;logging_public_IP&gt;</em> con tutti gli indirizzi delle regioni di registrazione per cui desideri consentire il traffico:
        <p><table summary="La prima riga nella tabella si estende su entrambe le colonne. Le righe rimanenti devono essere lette da sinistra a destra, con la zona server nella colonna uno e gli indirizzi IP corrispondenti nella colonna due.">
        <caption>Gli indirizzi IP da aprire per il traffico di registrazione</caption>
                <thead>
                <th>Regione {{site.data.keyword.containerlong_notm}}</th>
                <th>Indirizzo di registrazione</th>
                <th>Indirizzi IP di registrazione</th>
                </thead>
                <tbody>
                  <tr>
                    <td>Stati Uniti Est, Stati Uniti Sud</td>
                    <td><code>ingest.logging.ng.bluemix.net</code></td>
                    <td><code>169.48.79.236</code><br><code>169.46.186.113</code></td>
                  </tr>
                  <tr>
                   <td>Regno Unito Sud</td>
                   <td><code>ingest.logging.eu-gb.bluemix.net</code></td>
                   <td><code>169.50.115.113</code></td>
                  </tr>
                  <tr>
                   <td>Europa Centrale</td>
                   <td><code>ingest-eu-fra.logging.bluemix.net</code></td>
                   <td><code>158.177.88.43</code><br><code>159.122.87.107</code></td>
                  </tr>
                  <tr>
                   <td>Asia Pacifico Sud, Asia Pacifico Nord</td>
                   <td><code>ingest-au-syd.logging.bluemix.net</code></td>
                   <td><code>130.198.76.125</code><br><code>168.1.209.20</code></td>
                  </tr>
                 </tbody>
               </table></p>
    *   **{{site.data.keyword.la_full_notm}}**:
        <pre class="screen">TCP port 443, port 80 FROM &lt;each_worker_node_public_IP&gt; TO &lt;logDNA_public_IP&gt;</pre>
        Sostituisci `<logDNA_public_IP>` con gli [indirizzi IP LogDNA](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-network#network).

6. Se utilizzi i servizi del programma di bilanciamento del carico, assicurati che tutto il traffico che utilizza il protocollo VRRP sia consentito tra i nodi di lavoro sulle interfacce pubbliche e private. Red Hat OpenShift on IBM Cloud utilizza il protocollo VRRP per gestire gli indirizzi IP per i programmi di bilanciamento del carico pubblici e privati.

7. {: #pvc}Per creare le attestazioni del volume persistente in un cluster privato, assicurati che il tuo cluster sia configurato con la seguente versione di Kubernetes o con le seguenti versioni del plugin di archiviazione {{site.data.keyword.cloud_notm}}. Queste versioni abilitano le comunicazioni di rete privata dal tuo cluster alle istanze di archiviazione persistente.
    <table>
    <caption>Panoramica delle versioni di Kubernetes o del plugin di archiviazione {{site.data.keyword.cloud_notm}} richieste per i cluster privati</caption>
    <thead>
      <th>Tipo di archiviazione</th>
      <th>Versione richiesta</th>
   </thead>
   <tbody>
     <tr>
       <td>Archiviazione file</td>
       <td>Versione Kubernetes <code>1.13.4_1512</code>, <code>1.12.6_1544</code>, <code>1.11.8_1550</code>, <code>1.10.13_1551</code> o successiva</td>
     </tr>
     <tr>
       <td>Archiviazione blocchi</td>
       <td>Plugin {{site.data.keyword.cloud_notm}} Block Storage versione 1.3.0 o successive</td>
     </tr>
     <tr>
       <td>Archiviazione oggetti</td>
       <td><ul><li>Plugin {{site.data.keyword.cos_full_notm}} versione 1.0.3 o successive</li><li>Configurazione del servizio {{site.data.keyword.cos_full_notm}} con l'autenticazione HMAC</li></ul></td>
     </tr>
   </tbody>
   </table>

   Se devi utilizzare una versione Kubernetes o una versione del plugin di archiviazione {{site.data.keyword.cloud_notm}} che non supporta le comunicazioni di rete sulla rete privata o se vuoi utilizzare {{site.data.keyword.cos_full_notm}} senza l'autenticazione HMAC, consenti l'accesso in uscita tramite il tuo firewall all'infrastruttura IBM Cloud e a {{site.data.keyword.cloud_notm}} Identity and Access Management:
   - Consenti tutto il traffico di rete in uscita sulla porta TCP 443.
   - Consenti l'accesso all'intervallo di IP dell'infrastruttura IBM Cloud per la zona in cui si trova il tuo cluster sia per la [**Rete di front-end (pubblica)**](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#frontend-public-network) che per la [**Rete di back-end (privata)**](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#backend-private-network). Per trovare la zona del tuo cluster, esegui `ibmcloud oc clusters`.


<br />


## Concessione al cluster dell'accesso alle risorse su un firewall privato
{: #firewall_private}

Se hai un firewall sulla rete privata, consenti le comunicazioni tra i nodi di lavoro e consenti al tuo cluster l'accesso alle risorse dell'infrastruttura sulla rete privata.
{:shortdesc}

Vuoi utilizzare le politiche Calico perché fungano da tuo firewall del cluster invece di un firewall del dispositivo gateway? Vedi [Isolamento dei cluster sulla rete privata](/docs/containers?topic=containers-network_policies#isolate_workers).
{: tip}

1. Consenti tutto il traffico tra i nodi di lavoro.
    1. Consenti tutto il traffico TCP, UDP, VRRP e IPEncap tra i nodi di lavoro sulle interfacce pubbliche e private. Red Hat OpenShift on IBM Cloud utilizza il protocollo VRRP per gestire gli indirizzi IP per i programmi di bilanciamento del carico privati e il protocollo IPEncap per consentire il traffico tra i pod nelle sottoreti.
    2. Se utilizzi le politiche Calico, o se hai dei firewall in ciascuna zona di un cluster multizona, un firewall potrebbe bloccare le comunicazioni tra i nodi di lavoro. Devi aprire tutti i nodi di lavoro nel cluster tra di loro utilizzando le porte e gli indirizzi IP privati dei nodi di lavoro oppure l'etichetta di nodo di lavoro Calico.

2. Consenti gli intervalli di IP privati dell'infrastruttura IBM Cloud in modo da poter creare nodi di lavoro nel tuo cluster.
    1. Consenti gli intervalli di IP privati dell'infrastruttura IBM Cloud appropriati. Vedi [Rete di backend (privata)](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#backend-private-network).
    2. Consenti gli intervalli di IP privati dell'infrastruttura IBM Cloud per tutte le [zone](/docs/containers?topic=containers-regions-and-zones#zones) che stai utilizzando. **Nota**: devi aggiungere gli IP per le zone `dal01`, `dal10` e `wdc04` e, se il tuo cluster si trova nell'area geografica Europa, per la zona `ams01`. Vedi [Rete del servizio (nella rete di backend/privata)](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#service-network-on-backend-private-network-).

3. Apri le seguenti porte:
    - Consenti connessioni TCP e UDP in uscita dai nodi di lavoro alle porte 80 e 443 per consentire gli aggiornamenti e i ricaricamenti dei nodi di lavoro.
    - Consenti connessioni TCP e UDP in uscita alla porta 2049 per consentire il montaggio dell'archiviazione file come volumi.
    - Consenti connessioni TCP e UDP in uscita alla porta 3260 per le comunicazioni all'archiviazione blocchi.
    - Consenti connessioni TCP e UDP in entrata alla porta 10250 per il dashboard OpenShift e comandi come `oc logs` e `oc exec`.
    - Consenti connessioni in entrata e in uscita TCP e UDP alla porta 53 per l'accesso DNS.

4. Se hai anche un firewall sulla rete pubblica o se hai un cluster solo VLAN privata e stai utilizzando un dispositivo gateway come firewall, devi consentire anche gli IP e le porte specificati in [Concessione al cluster dell'accesso alle risorse dell'infrastruttura e ad altri servizi](#firewall_outbound).

<br />


## Concessione al cluster dell'accesso alle risorse attraverso le politiche in uscita
Calico
{: #firewall_calico_egress}

Se utilizzi le [politiche di rete Calico](/docs/containers?topic=containers-network_policies) perché fungano da firewall per limitare tutta l'uscita di nodo di lavoro pubblico, devi consentire ai tuoi nodi di lavoro di accedere alle sottoreti necessarie per il funzionamento del cluster.
{: shortdesc}

Per utilizzare le politiche Calico perché fungano da tuo firewall del cluster sulla rete pubblica, devi applicare le politiche in [Isolamento dei cluster sulla rete pubblica](/docs/containers?topic=containers-network_policies#isolate_workers_public).

Per utilizzare le politiche Calico perché fungano da tuo firewall del cluster sulla rete privata, devi applicare le politiche in [Isolamento dei cluster sulla rete privata](/docs/containers?topic=containers-network_policies#isolate_workers).

<br />


## Accesso ai servizi NodePort, programma di bilanciamento del carico e Ingress dall'esterno del cluster
{: #firewall_inbound}

Puoi ora consentire l'accesso in entrata ai servizi NodePort, programma di bilanciamento del carico e Ingress.
{:shortdesc}

<dl>
  <dt>Servizio NodePort</dt>
  <dd>Apri la porta che hai configurato quando hai distribuito il servizio agli indirizzi IP pubblici per tutti i nodi di lavoro a cui consentire il traffico. Per trovare la porta, esegui `oc get svc`. La porta è compresa nell'intervallo 20000-32000.<dd>
  <dt>Servizio del programma di bilanciamento del carico</dt>
  <dd>Apri la porta che hai configurato quando hai distribuito il servizio all'indirizzo IP pubblico del servizio del programma di bilanciamento del carico.</dd>
  <dt>Ingress</dt>
  <dd>Apri la porta 80 per HTTP o la 443 per HTTPS per l'indirizzo IP per l'ALB (application load balancer) Ingress.</dd>
</dl>

<br />


## Inserimento in whitelist del tuo cluster nei firewall di altri servizi o nei firewall in loco
{: #whitelist_workers}

Se vuoi accedere a servizi eseguiti all'interno o all'esterno di {{site.data.keyword.cloud_notm}} o in loco e che sono protetti da un firewall, puoi aggiungere gli indirizzi IP dei tuoi nodi di lavoro in tale firewall per consentire il traffico di rete in uscita verso il tuo cluster. Ad esempio, potresti voler leggere i dati da un database {{site.data.keyword.cloud_notm}} protetto da un firewall o inserire nella whitelist le sottoreti del nodo di lavoro in un firewall in loco per consentire il traffico di rete dal tuo cluster.
{:shortdesc}

1.  [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

2. Ottieni le sottoreti o gli indirizzi IP del nodo di lavoro.
  * **Sottoreti del nodo di lavoro**: se prevedi di modificare frequentemente il numero di nodi di lavoro nel tuo cluster, ad esempio se abiliti il [cluster autoscaler](/docs/containers?topic=containers-ca#ca), potresti non voler aggiornare il firewall per ogni nuovo nodo di lavoro. Puoi invece inserire nella whitelist le sottoreti VLAN utilizzate dal cluster. Tieni presente che la sottorete VLAN potrebbe essere condivisa da nodi di lavoro in altri cluster.
    <p class="note">Le **sottoreti pubbliche primarie** di cui Red Hat OpenShift on IBM Cloud esegue il provisioning per il tuo cluster vengono fornite con 14 indirizzi IP disponibili e possono essere condivise da altri cluster sulla stessa VLAN. Se hai più di 14 nodi di lavoro, viene ordinata un'altra sottorete, per cui le sottoreti che devi inserire nella whitelist possono cambiare. Per ridurre la frequenza delle modifiche, crea pool di nodi di lavoro con profili di nodi di lavoro con risorse CPU e memoria più elevate in modo da non dover aggiungere nodi tanto spesso.</p>
    1. Elenca i nodi di lavoro nel tuo cluster.
      ```
      ibmcloud oc workers --cluster <cluster_name_or_ID>
      ```
      {: pre}

    2. Dall'output del passo precedente, prendi nota di tutti gli ID di rete univoci (primi tre ottetti) dell'**IP pubblico** per i nodi di lavoro nel tuo cluster. Se vuoi inserire in whitelist un cluster solo privato, prendi invece nota dell'**IP privato** . Nel seguente output, gli ID di rete univoci sono `169.xx.178` e `169.xx.210`.
        ```
        ID                                                  Public IP        Private IP     Machine Type        State    Status   Zone    Version   
        kube-dal10-crb2f60e9735254ac8b20b9c1e38b649a5-w31   169.xx.178.101   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal10   1.13.8   
        kube-dal10-crb2f60e9735254ac8b20b9c1e38b649a5-w34   169.xx.178.102   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal10   1.13.8  
        kube-dal12-crb2f60e9735254ac8b20b9c1e38b649a5-w32   169.xx.210.101   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal12   1.13.8   
        kube-dal12-crb2f60e9735254ac8b20b9c1e38b649a5-w33   169.xx.210.102   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal12   1.13.8  
        ```
        {: screen}
    3.  Elenca le sottoreti VLAN per ogni ID di rete univoco.
        ```
        ibmcloud sl subnet list | grep -e <networkID1> -e <networkID2>
        ```
        {: pre}

        Output di esempio:
        ```
        ID        identifier       type                 network_space   datacenter   vlan_id   IPs   hardware   virtual_servers
        1234567   169.xx.210.xxx   ADDITIONAL_PRIMARY   PUBLIC          dal12        1122334   16    0          5   
        7654321   169.xx.178.xxx   ADDITIONAL_PRIMARY   PUBLIC          dal10        4332211   16    0          6    
        ```
        {: screen}
    4.  Richiama l'indirizzo di sottorete. Nell'output, trova il numero di **IP**. Quindi, eleva `2` alla potenza di `n` uguale al numero di IP. Ad esempio, se il numero di IP è `16`, `2` viene elevato alla potenza di `4` (`n`) uguale a `16`. Ora ottieni il CIDR della sottorete sottraendo il valore di `n` da `32` bit. Ad esempio, se `n` è uguale a `4`, il CIDR è `28` (dall'equazione `32 - 4 = 28`). Combina la maschera dell'**identificativo** con il valore CIDR per ottenere l'indirizzo completo della sottorete. Nell'output precedente, gli indirizzi di sottorete sono:
        *   `169.xx.210.xxx/28`
        *   `169.xx.178.xxx/28`
  * **Indirizzi IP dei singoli nodi di lavoro**: se hai un numero ridotto di nodi di lavoro che eseguono solo un'applicazione e non richiedono un ridimensionamento o se vuoi inserire nella whitelist solo un nodo di lavoro, elenca tutti i nodi di lavoro nel tuo cluster e prendi nota degli indirizzi **IP pubblici**. Se i tuoi nodi di lavoro sono connessi solo a una rete privata e vuoi connetterti ai servizi {{site.data.keyword.cloud_notm}} utilizzando l'endpoint del servizio privato, prendi nota degli indirizzi **IP privati**. Solo questi nodi di lavoro sono inseriti nella whitelist. Se elimini o aggiungi nodi di lavoro nel cluster, devi aggiornare il tuo firewall di conseguenza.
    ```
    ibmcloud oc workers --cluster <cluster_name_or_ID>
    ```
    {: pre}
4.  Aggiungi il CIDR della sottorete o gli indirizzi IP al firewall del tuo servizio per il traffico in uscita o al firewall in loco per il traffico in entrata.
5.  Ripeti questi passi per ciascun cluster che vuoi inserire nella whitelist.


