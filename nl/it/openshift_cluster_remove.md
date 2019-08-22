---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhos, rhoks, clusters, worker nodes, worker pools, delete

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

# Rimozione dei cluster
{: #remove}

I cluster gratuiti e standard creati con un account fatturabile devono essere rimossi manualmente quando non sono più necessari in modo che non consumino più le risorse.
{:shortdesc}

<p class="important">
Non viene creato alcun backup del tuo cluster o dei tuoi dati nella tua archiviazione persistente. Quando elimini un cluster, puoi scegliere di eliminare la tua archiviazione persistente. Se scegli di eliminarla, l'archiviazione persistente di cui hai eseguito il provisioning utilizzando una classe di archiviazione `delete` viene eliminata in modo permanente dall'infrastruttura IBM Cloud. Se hai eseguito il provisioning dell'archiviazione persistente utilizzando una classe di archiviazione `retain` e scegli di eliminare la tua archiviazione, il cluster, il PV e la PVC vengono eliminati, ma l'istanza dell'archiviazione persistente rimane nel tuo account dell'infrastruttura IBM Cloud</br>
</br>Quando rimuovi un cluster, rimuovi anche le sottoreti di cui è stato eseguito automaticamente il provisioning quando hai creato il cluster e che hai creato utilizzando il comando `ibmcloud oc cluster-subnet-create`. Tuttavia, se hai aggiunto manualmente sottoreti esistenti al tuo cluster utilizzando il `comando ibmcloud oc cluster-subnet-add`, tali sottoreti non verranno rimosse dal tuo account dell'infrastruttura IBM Cloud e potrai riutilizzarle in altri cluster.</p>

Prima di iniziare:
* Prendi nota del tuo ID cluster. Potresti aver bisogno dell'ID cluster per analizzare e rimuovere le risorse correlate all'infrastruttura IBM Cloud che non vengono automaticamente eliminate con il tuo cluster.
* Se vuoi eliminare i dati nella tua archiviazione persistente, [comprendi le opzioni di eliminazione](/docs/containers?topic=containers-cleanup#cleanup).
* Assicurati di disporre del [ruolo della piattaforma {{site.data.keyword.cloud_notm}} IAM **Amministratore**](/docs/containers?topic=containers-users#platform).

Per rimuovere un cluster:
 
1. Facoltativo: dalla CLI, salva una copia di tutti i dati nel tuo cluster in un file YAML locale.
  ```
  oc get all --all-namespaces -o yaml
  ```
  {: pre}

2. Rimuovi il cluster.
  - Dalla console {{site.data.keyword.cloud_notm}}
    1.  Seleziona il tuo cluster e fai clic su **Elimina** dal menu **Ulteriori azioni...**.

  - Dalla CLI {{site.data.keyword.cloud_notm}}
    1.  Elenca i cluster disponibili.

        ```
        ibmcloud oc clusters
        ```
        {: pre}

    2.  Elimina il cluster.

        ```
        ibmcloud oc cluster-rm --cluster <cluster_name_or_ID>
        ```
        {: pre}

    3.  Segui le richieste e scegli se eliminare le risorse del cluster che includono contenitori, pod, servizi associati, archiviazione persistente e segreti.
      - **Archiviazione persistente**: l'archiviazione persistente fornisce l'alta disponibilità per i tuoi dati. Se hai creato un'attestazione del volume persistente utilizzando una [condivisione file esistente](/docs/containers?topic=containers-file_storage#existing_file), non potrai eliminare la condivisione file quando elimini il cluster. Devi eliminare manualmente in seguito la condivisione file dal tuo portfolio dell'infrastruttura IBM Cloud.

          A causa del ciclo di fatturazione mensile, non è possibile eliminare un'attestazione del volume persistente durante l'ultimo giorno del mese. Se elimini l'attestazione del volume persistente l'ultimo giorno del mese, l'eliminazione rimane in sospeso fino all'inizio del mese successivo.
          {: note}

Passi successivi:
- Puoi riutilizzare il nome di un cluster rimosso una volta che non è più presente nell'elenco dei cluster disponibili quando viene eseguito il comando `ibmcloud oc clusters`.
- Se mantieni le sottoreti, puoi [riutilizzarle in un nuovo cluster](/docs/containers?topic=containers-subnets#subnets_custom) o eliminarle manualmente in un secondo momento dal tuo portfolio dell'infrastruttura IBM Cloud.
- Se mantieni l'archiviazione persistente, puoi [eliminare la tua archiviazione](/docs/containers?topic=containers-cleanup#cleanup) in un secondo momento attraverso il dashboard dell'infrastruttura IBM Cloud nella console {{site.data.keyword.cloud_notm}}.



