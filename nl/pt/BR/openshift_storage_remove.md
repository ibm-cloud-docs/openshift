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
 
# Removendo o armazenamento persistente de um cluster
{: #cleanup}

Ao configurar o armazenamento persistente em seu cluster, você tem três componentes principais: a solicitação de volume persistente do Kubernetes (PVC) que solicita o armazenamento, o volume persistente do Kubernetes (PV) que é montado em um pod e descrito no PVC e a instância de infraestrutura do IBM Cloud, como arquivo NFS ou armazenamento de bloco. Dependendo de como você criou seu armazenamento, pode ser necessário excluir todos os três separadamente.
{:shortdesc}

## Limpando o armazenamento persistente
{: #storage_remove}

Entendendo suas opções de exclusão:

** Eu excluo meu cluster. Preciso excluir alguma outra coisa para remover o armazenamento persistente?**</br>
Depende. Quando você exclui um cluster, o PVC e o PV são excluídos. No entanto, você escolhe se deve remover a instância de armazenamento associada na infraestrutura do IBM Cloud. Se você escolheu não a remover, a instância de armazenamento ainda existe. Além disso, se você excluiu seu cluster em um estado não funcional, o armazenamento ainda poderá existir mesmo se você escolheu removê-lo. Siga as instruções, particularmente a etapa para [excluir sua instância de armazenamento](#sl_delete_storage) na infraestrutura do IBM Cloud.

**Posso excluir a PVC para remover todo o meu armazenamento?**</br>
Às vezes. Se você [criar o armazenamento persistente dinamicamente](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) e selecionar uma classe de armazenamento sem `retain` em seu nome, quando você excluir o PVC, o PV e a instância de armazenamento da infraestrutura do IBM Cloud também serão excluídos.

Em todos os outros casos, siga as instruções para verificar o status de seu PVC, PV e o dispositivo de armazenamento físico e exclua-os separadamente, se necessário.

**Ainda estou cobrado pelo armazenamento depois de excluí-lo?**</br>
Depende do que você excluir e do tipo de faturamento. Se você excluir o PVC e o PV, mas não a instância em sua conta de infraestrutura do IBM Cloud, essa instância ainda existirá e você será cobrado por ela. Deve-se excluir tudo para evitar encargos. Além disso, quando você especifica o `billingType` no PVC, é possível escolher `hourly` ou `monthly`. Se você escolheu `monthly`, sua instância será faturada mensalmente. Quando você excluir a instância, será cobrado pelo restante do mês.

Ao cancelar manualmente a instância de armazenamento persistente por meio do console de infraestrutura do IBM Cloud ou da CLI `ibmcloud sl`, o faturamento é interrompido da seguinte forma: 
- **Armazenamento por hora**: o faturamento é interrompido imediatamente. Depois que seu armazenamento for cancelado, você ainda poderá ver sua instância de armazenamento no console por até 72 horas.  
- **Armazenamento mensal**: é possível escolher entre **cancelamento imediato** ou **cancelamento na data do aniversário**. Se você escolher cancelamento imediato, seu armazenamento será removido imediatamente e não será mais possível usar seu armazenamento. Se você optar por cancelar seu armazenamento na data do próximo aniversário, suas instâncias de armazenamento permanecerão ativas até a data do próximo aniversário e você poderá continuar a usá-las até essa data. Em ambos os casos, o faturamento é interrompido para o próximo ciclo de faturamento, mas você ainda é faturado até o final do ciclo de faturamento atual. Depois que seu armazenamento for cancelado, você ainda poderá ver sua instância de armazenamento no console ou na CLI por até 72 horas.  

Se você remover o armazenamento persistente com uma política de recuperação `Delete` que você provisionou dinamicamente excluindo o PVC, o armazenamento será removido imediatamente independentemente de você ter escolhido um tipo de faturamento por hora ou mensal. Após o armazenamento ser removido, você ainda poderá ver sua instância de armazenamento no console ou na CLI por até 72 horas. O armazenamento persistente que usa uma política de recuperação `Retain` não é removido e você ainda é cobrado por utilizá-lo. 

<p class="important">Ao limpar o armazenamento persistente, você exclui todos os dados que estão armazenados nele. Se você precisar de uma cópia dos dados, faça um backup para o [armazenamento de arquivo](/docs/containers?topic=containers-file_storage#file_backup_restore) ou [armazenamento de bloco](/docs/containers?topic=containers-block_storage#block_backup_restore).  </p>

**Eu excluí meu armazenamento. Por que ainda posso ver minhas instâncias?**</br>
Depois de remover o armazenamento persistente, ele pode demorar até 72 horas para que a remoção seja completamente processada e para que o armazenamento desapareça do console ou da CLI de infraestrutura do IBM Cloud. 

Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

Para limpar os dados persistentes:

1.  Liste os PVCs em seu cluster e anote o **`NAME`** do PVC, o **`STORAGECLASS`** e o nome do PV que está ligado ao PVC e mostrado como **`VOLUME`**.
    ```
    oc get pvc
    ```
    {: pre}

    Saída de exemplo:
    ```
    NAME                  STATUS    VOLUME                                     CAPACITY   ACCESSMODES   STORAGECLASS            AGE
    claim1-block-bronze   Bound     pvc-06886b77-102b-11e8-968a-f6612bb731fb   20Gi       RWO           ibmc-block-bronze       78d
    claim-file-bronze     Bound     pvc-457a2b96-fafc-11e7-8ff9-b6c8f770356c   4Gi        RWX           ibmc-file-bronze-retain 105d
    claim-file-silve      Bound     pvc-1efef0ba-0c48-11e8-968a-f6612bb731fb   24Gi       RWX           ibmc-file-silver        83d
    ```
    {: screen}

2. Revise o **`ReclaimPolicy`** e o **`billingType`** para a classe de armazenamento.
   ```
   oc describe storageclass <storageclass_name>
   ```
   {: pre}

   Se a política de recuperação indicar `Delete`, seu PV e o armazenamento físico serão removidos quando você remover o PVC. Se a política de recuperação indicar `Retain` ou se você provisionar o armazenamento sem uma classe de armazenamento, o PV e o armazenamento físico não serão removidos quando o PVC for removido. Deve-se remover o PVC, o PV e o armazenamento físico separadamente.

   Se o seu armazenamento for cobrado mensalmente, você ainda será cobrado pelo mês inteiro, mesmo se remover o armazenamento antes do término do ciclo de faturamento.
   {: important}

3. Remova quaisquer pods que montam o PVC.
   1. Liste os pods que montam o PVC.
      ```
      oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
      ```
      {: pre}

      Saída de exemplo:
      ```
      blockdepl-12345-prz7b: claim1-block-bronze  
      ```
      {: screen}

      Se nenhum pod é retornado em sua saída da CLI, você não tem um pod que usa o PVC.

   2. Remova o pod que usa o PVC. Se o pod fizer parte de uma implementação, remova a implementação.
      ```
      oc delete pod <pod_name>
      ```
      {: pre}

   3. Verifique se o pod foi removido.
      ```
      oc get pods
      ```
      {: pre}

4. Remova o PVC.
   ```
   oc delete pvc <pvc_name>
   ```
   {: pre}

5. Revise o status de seu PV. Use o nome do PV que você recuperou anteriormente como **`VOLUME`**.
   ```
   oc get pv <pv_name>
   ```
   {: pre}

   Quando você remove o PVC, o PV que está ligado ao PVC é liberado. Dependendo de como você provisionou seu armazenamento, seu PV entrará em um estado `Deleting` se o PV for excluído automaticamente ou em um estado `Released` se o PV deverá ser excluído manualmente. **Nota**: para PVs que são excluídos automaticamente, o status pode indicar brevemente `Released` antes de ser excluído. Execute novamente o comando após alguns minutos para ver se o PV foi removido.

6. Se o seu PV não for excluído, remova-o manualmente.
   ```
   oc delete pv <pv_name>
   ```
   {: pre}

7. Verifique se o PV foi removido.
   ```
   oc get pv
   ```
   {: pre}

8. {: #sl_delete_storage}Liste a instância de armazenamento físico para a qual seu PV apontou e anote o **`id`** da instância de armazenamento físico.

   **Armazenamento de arquivo:**
   ```
   ibmcloud sl file volume-list --columns id  --columns notes | grep <pv_name>
   ```
   {: pre}
   **Armazenamento de bloco:**
   ```
   ibmcloud sl block volume-list --columns id --columns notes | grep <pv_name>
   ```
   {: pre}

   Se você removeu seu cluster e não consegue recuperar o nome do PV, substitua `grep <pv_name>` por `grep <cluster_id>` para listar todos os dispositivos de armazenamento associados ao seu cluster.
   {: tip}

   Saída de exemplo:
   ```
   id         notes   
   12345678   {"plugin":"ibm-file-plugin-5b55b7b77b-55bb7","region":"us-south","cluster":"aa1a11a1a11b2b2bb22b22222c3c3333","type":"Endurance","ns":"default","pvc":"mypvc","pv":"pvc-d979977d-d79d-77d9-9d7d-d7d97ddd99d7","storageclass":"ibmc-file-gold"}
   ```
   {: screen}

   Entendendo as informações do campo do **Notas**:
   *  **`"plugin":"ibm-file-plugin-5b55b7b77b-55bb7"`**: o plug-in de armazenamento que o cluster usa.
   *  **`"region":"us-south"`**: a região em que seu cluster está.
   *  **`"cluster":"aa1a11a1a11b2b2bb22b22222c3c3333"`**: o ID do cluster que está associado à instância de armazenamento.
   *  **`"type":"Endurance"`**: o tipo de armazenamento de arquivo ou de bloco `Endurance` ou `Performance`.
   *  **`"ns":"default"`**: o namespace no qual a instância de armazenamento é implementada.
   *  **`"pvc": "mypvc"`**: O nome do PVC que está associado com a instância de armazenamento.
   *  **`"pv":"pvc-d979977d-d79d-77d9-9d7d-d7d97ddd99d7"`**: o PV que está associado à instância de armazenamento.
   *  **`"storageclass":"ibmc-file-gold"`**: o tipo de classe de armazenamento: bronze, prata, ouro ou customizado.

9. Remova a instância de armazenamento físico.

   **Armazenamento de arquivo:**
   ```
   ibmcloud sl file volume-cancel <filestorage_id>
   ```
   {: pre}

   **Armazenamento de bloco:**
   ```
   ibmcloud sl block volume-cancel <blockstorage_id>
   ```
   {: pre}

10. Verifique se a instância de armazenamento físico foi removida. 
   
   O processo de exclusão pode levar até 72 horas para ser concluído.
   {: important}

   **Armazenamento de arquivo:**
   ```
   ibmcloud sl file volume-list
   ```
   {: pre}
   **Armazenamento de bloco:**
   ```
   ibmcloud sl block volume-list
   ```
   {: pre}


