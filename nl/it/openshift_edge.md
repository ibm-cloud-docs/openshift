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

# Limitazione del traffico di rete ai nodi di lavoro edge
{: #edge}

I nodi di lavoro edge possono migliorare la sicurezza del tuo cluster {{site.data.keyword.openshiftlong}} consentendo a un minor numero di nodi di lavoro di essere accessibili esternamente e isolando il carico di lavoro della rete.
{:shortdesc}

Quando questi nodi di lavoro sono contrassegnati solo per la rete, gli altri carichi di lavoro non possono consumare la CPU o la memoria del nodo di lavoro e interferire con la rete.

Se hai un cluster multizona e vuoi limitare il traffico di rete ai nodi di lavoro edge, è necessario abilitare almeno due nodi di lavoro edge in ogni zona per l'alta disponibilità dei pod del programma di bilanciamento del carico e dei pod Ingress. Crea un pool di nodi di lavoro del nodo edge che si estenda su tutte le zone del tuo cluster, con almeno due nodi di lavoro per zona.
{: tip}

## Etichettatura dei nodi di lavoro come nodi edge
{: #edge_nodes}

Aggiungi l'etichetta `dedicated=edge` a due o più nodi di lavoro su ogni VLAN pubblica o privata nel tuo cluster per garantire che gli NLB (network load balancer) e gli ALB (application load balancer) Ingress vengano distribuiti solo a quei nodi di lavoro.
{:shortdesc}

**Cluster Kubernetes della community**: in Kubernetes 1.14 e versioni successive, è possibile distribuire gli NLB e gli ALB sia pubblici che privati ai nodi di lavoro edge. In Kubernetes 1.13 e versioni precedenti, gli ALB pubblici e privati e gli NLB pubblici possono essere distribuiti ai nodi edge, ma gli NLB privati devono essere distribuiti solo ai nodi di lavoro non edge nel tuo cluster.
{: note}

Prima di iniziare:

* Assicurati di disporre dei seguenti [ruoli {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-users#platform):
  * Qualsiasi ruolo della piattaforma per il cluster
  * Ruolo del servizio **Scrittore** o **Gestore** per tutti gli spazi dei nomi
* [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

</br>Per etichettare i nodi di lavoro come nodi edge:

1. [Crea un nuovo pool di nodi di lavoro](/docs/containers?topic=containers-add_workers#add_pool) che si estenda su tutte le zone del tuo cluster e che abbia almeno due nodi di lavoro per zona. Nel comando `ibmcloud oc worker-pool-create`, includi l'indicatore `--labels dedicated=edge` per etichettare tutti i nodi di lavoro nel pool. Tutti i nodi di lavoro in questo pool, inclusi i nodi di lavoro che aggiungi in seguito, vengono etichettati come nodi edge. Una volta che il pool di nodi di lavoro è contrassegnato con `dedicated=edge`, tutti i nodi di lavoro esistenti e successivi ottengono questa etichetta e i servizi Ingress e di programma di bilanciamento del carico vengono distribuiti su un nodo di lavoro edge.
  <p class="tip">Se vuoi utilizzare un pool di nodi di lavoro esistente, il pool deve estendersi su tutte le zone del tuo cluster e avere almeno due nodi di lavoro per zona. Puoi etichettare il pool di nodi di lavoro con `dedicated=edge` utilizzando l'[API del pool di nodi di lavoro PATCH](https://containers.cloud.ibm.com/global/swagger-global-api/#/clusters/PatchWorkerPool). Nel corpo della richiesta, passa il seguente JSON.
      <pre class="screen">
      {
        "labels": {"dedicated":"edge"},
        "state": "labels"
      }</pre></p>

2. Verifica che il pool di nodi di lavoro e i nodi di lavoro abbiano l'etichetta `dedicated=edge`.
  * Per controllare il pool di nodi di lavoro:
    ```
    ibmcloud oc worker-pool-get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
    ```
    {: pre}

  * Per controllare i singoli nodi di lavoro, riesamina il campo **Labels** dell'output del seguente comando.
    ```
    oc describe node <worker_node_private_IP>
    ```
    {: pre}

3. Richiama tutti gli NLB e ALB esistenti nel cluster.
  ```
  oc get services --all-namespaces | grep LoadBalancer
  ```
  {: pre}

  Nell'output, nota lo **Spazio dei nomi** e il **Nome** di ogni servizio del programma di bilanciamento del carico. Ad esempio, nel seguente output, ci sono quattro servizi del programma di bilanciamento del carico: un NLB pubblico nello spazio dei nomi `default` e un ALB privato e due ALB pubblici nello spazio dei nomi `kube-system`.
  ```
  NAMESPACE     NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
  default       webserver-lb                                     LoadBalancer   172.21.190.18    169.46.17.2     80:30597/TCP                                10m
  kube-system   private-crdf253b6025d64944ab99ed63bb4567b6-alb1  LoadBalancer   172.21.158.78    10.185.94.150   80:31015/TCP,443:31401/TCP,9443:32352/TCP   25d
  kube-system   public-crdf253b6025d64944ab99ed63bb4567b6-alb1   LoadBalancer   172.21.84.248    169.48.228.78   80:30286/TCP,443:31363/TCP                  25d
  kube-system   public-crdf253b6025d64944ab99ed63bb4567b6-alb2   LoadBalancer   172.21.229.73    169.46.17.6     80:31104/TCP,443:31138/TCP                  25d
  ```
  {: screen}

4. Utilizzando l'output dal passo precedente, immetti il seguente comando per ogni NLB e ALB. Questo comando ridistribuisce l'NLB o l'ALB a un nodo di lavoro edge.

  **Cluster Kubernetes della community**: se il tuo cluster esegue Kubernetes 1.14 o versioni successive, puoi distribuire gli NLB e gli ALB sia pubblici che privati ai nodi di lavoro edge. In Kubernetes 1.13 e versioni precedenti, solo gli ALB pubblici e privati e gli NLB pubblici possono essere distribuiti ai nodi edge, pertanto non ridistribuire i servizi NLB privati.
  {: note}

  ```
  oc get service -n <namespace> <service_name> -o yaml | oc apply -f -
  ```
  {: pre}

  Output di esempio:
  ```
  service "webserver-lb" configured
  ```
  {: screen}

5. Per verificare che i carichi di lavoro di rete siano limitati ai nodi edge, conferma che i pod NLB e ALB siano pianificati sui nodi edge e che non siano pianificati sui nodi non edge.

  * Pod NLB:
    1. Conferma che i pod NLB siano distribuiti ai nodi edge. Cerca l'indirizzo IP esterno del servizio del programma di bilanciamento del carico che è elencato nell'output del passo 3. Sostituisci i punti (`.`) con i trattini (`-`). Esempio per l'NLB `webserver-lb` con indirizzo IP esterno `169.46.17.2`:
      ```
      oc describe nodes -l dedicated=edge | grep "169-46-17-2"
      ```
      {: pre}

      Output di esempio:
      ```
      ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
      ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
      ```
      {: screen}
    2. Conferma che nessun pod NLB sia distribuito ai nodi non edge. Esempio per l'NLB `webserver-lb` con indirizzo IP esterno `169.46.17.2`:
      ```
      oc describe nodes -l dedicated!=edge | grep "169-46-17-2"
      ```
      {: pre}
      * Se i pod NLB vengono distribuiti correttamente ai nodi edge, non viene restituito alcun pod NLB. I tuoi NLB vengono ripianificati correttamente solo sui nodi di lavoro edge.
      * Se i pod NLB vengono restituiti, vai al passo successivo.

  * Pod ALB:
    1. Conferma che tutti i pod ALB siano distribuiti ai nodi edge. Cerca la parola chiave `alb`. Ogni ALB pubblico e privato ha due pod. Esempio:
      ```
      oc describe nodes -l dedicated=edge | grep alb
      ```
      {: pre}

      Output di esempio per un cluster con due zone in cui sono abilitati un ALB privato predefinito e due ALB pubblici predefiniti:
      ```
      kube-system                private-crdf253b6025d64944ab99ed63bb4567b6-alb1-d5dd478db-27pv4    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                private-crdf253b6025d64944ab99ed63bb4567b6-alb1-d5dd478db-7p9q6    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb1-5ff8cdff89-s77z6    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb1-5ff8cdff89-kvs9f    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb2-57df7c7b5b-tp6xw    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb2-57df7c7b5b-z5p2v    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      ```
      {: screen}

    2. Conferma che nessun pod ALB sia distribuito ai nodi non edge. Esempio:
      ```
      oc describe nodes -l dedicated!=edge | grep alb
      ```
      {: pre}
      * Se i pod ALB vengono distribuiti correttamente ai nodi edge, non viene restituito alcun pod ALB. I tuoi ALB vengono ripianificati correttamente solo sui nodi di lavoro edge.
      * Se i pod ALB vengono restituiti, vai al passo successivo.

6. Se i pod NLB o ALB vengono ancora distribuiti a nodi non edge, puoi eliminare i pod in modo che vengano ridistribuiti ai nodi edge. **Importante**: elimina solo un pod alla volta e verifica che il pod sia ripianificato su un nodo edge prima di eliminare gli altri pod.
  1. Elimina un pod. Esempio per il caso in cui uno dei pod NLB `webserver-lb` non sia stato pianificato su un nodo edge:
    ```
    oc delete pod ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg
    ```
    {: pre}

  2. Verifica che il pod venga ripianificato su un nodo di lavoro edge. La ripianificazione è automatica, ma potrebbe richiedere alcuni minuti. Esempio per l'NLB `webserver-lb` con indirizzo IP esterno `169.46.17.2`:
    ```
    oc describe nodes -l dedicated=edge | grep "169-46-17-2"
    ```
    {: pre}

    Output di esempio:
    ```
    ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
    ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
    ```
    {: screen}

</br>Hai etichettato i nodi di lavoro in un pool con `dedicated=edge` e hai ridistribuito tutti gli ALB e NLB esistenti ai nodi edge. Tutti i successivi ALB e NLB che vengono aggiunti al cluster vengono anche distribuiti a un nodo edge nel tuo pool di nodi di lavoro edge. Successivamente, impedisci [l'esecuzione di altri carichi di lavoro sui nodi di lavoro edge](#edge_workloads) e [blocca il traffico in entrata verso le NodePort sui nodi di lavoro](/docs/containers?topic=containers-network_policies#block_ingress).

<br />


## Blocco dell'esecuzione dei carichi di lavoro sui nodi di lavoro edge
{: #edge_workloads}

Uno dei vantaggi dei nodi di lavoro edge è che possono essere specificati per eseguire solo i servizi di rete.
{:shortdesc}

L'utilizzo della tolleranza `dedicated=edge` indica che tutti i servizi NLB (network load balancer) e ALB (application load balancer) Ingress vengono distribuiti solo ai nodi di lavoro etichettati. Tuttavia, per impedire che altri carichi di lavoro vengano eseguiti sui nodi di lavoro edge e consumino le risorse dei nodi di lavoro, devi utilizzare le [contaminazioni Kubernetes ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/).

Prima di iniziare:
- Assicurati di disporre del [ruolo del servizio {{site.data.keyword.cloud_notm}} IAM **Gestore** per tutti gli spazi dei nomi](/docs/containers?topic=containers-users#platform).
- [Accedi al tuo account. Se applicabile, specifica il gruppo di risorse appropriato. Imposta il contesto per il tuo cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

</br>Per impedire l'esecuzione di altri carichi di lavoro sui nodi di lavoro edge:

1. Applica una contaminazione a tutti i nodi di lavoro con l'etichetta `dedicated=edge` che impedisca ai pod di essere eseguiti sul nodo di lavoro e che rimuova i pod che non hanno l'etichetta `dedicated=edge` dal nodo di lavoro. I pod che vengono rimossi vengono ridistribuiti ad altri nodi di lavoro con capacità.
  ```
  oc taint node -l dedicated=edge dedicated=edge:NoSchedule dedicated=edge:NoExecute
  ```
  {: pre}
  Adesso, solo i pod con la tolleranza `dedicated=edge` vengono distribuiti ai tuoi nodi di lavoro edge.

2. Verifica che i tuoi nodi edge siano contaminati.
  ```
  oc describe nodes -l dedicated=edge | grep "Taint|Hostname"
  ```
  {: pre}

  Output di esempio:
  ```
  Taints:             dedicated=edge:NoExecute
    Hostname:    10.176.48.83
  Taints:             dedicated=edge:NoExecute
    Hostname:    10.184.58.7
  ```
  {: screen}

3. Se scegli di [abilitare la conservazione dell'IP di origine per un servizio NLB 1.0](/docs/containers?topic=containers-loadbalancer#node_affinity_tolerations), assicurati che i pod dell'applicazione vengano pianificati sui nodi di lavoro edge [aggiungendo l'affinità del nodo edge ai pod dell'applicazione](/docs/containers?topic=containers-loadbalancer#lb_edge_nodes). I pod dell'applicazione devono essere pianificati nei nodi edge per ricevere le richieste in entrata.

4. Per rimuovere una contaminazione, immetti questo comando.
    ```
    oc taint node <node_name> dedicated:NoSchedule- dedicated:NoExecute-
    ```
    {: pre}


