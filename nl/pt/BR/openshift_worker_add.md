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

# Incluindo nós do trabalhador e zonas em clusters
{: #add_workers}

Para aumentar a disponibilidade de seus apps, é possível incluir nós do trabalhador em uma zona existente ou em múltiplas zonas existentes em seu cluster. Para ajudar a proteger seus apps contra falhas de zona, é possível incluir zonas em seu cluster.
{:shortdesc}

Quando você cria um cluster, os nós do trabalhador são provisionados em um conjunto de trabalhadores. Após a criação do cluster, é possível incluir mais nós do trabalhador em um conjunto, redimensionando-o ou incluindo mais conjuntos de trabalhadores. Por padrão, o conjunto de trabalhadores existe em uma zona. Os clusters que têm um conjunto de trabalhadores em somente uma zona são chamados de clusters de zona única. Quando você incluir mais zonas no cluster, o conjunto de trabalhadores existirá entre as zonas. Os clusters que têm um conjunto de trabalhadores que é difundido em mais de uma zona são chamados de clusters de múltiplas zonas.

Se você tiver um cluster de múltiplas zonas, mantenha seus recursos do nó do trabalhador balanceados. Certifique-se de que todos os conjuntos de trabalhadores estejam difundidos pelas mesmas zonas e inclua ou remova os trabalhadores redimensionando os conjuntos em vez de incluir nós individuais.
{: tip}

Antes de iniciar, certifique-se de que tenha a função da plataforma [**Operador** ou **Administrador** do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-users#platform). Em seguida, escolha uma das seções a seguir:
  * [Incluir nós do trabalhador redimensionando um conjunto de trabalhadores existente em seu cluster](#resize_pool)
  * [Incluir nós do trabalhador incluindo um conjunto de trabalhadores em seu cluster](#add_pool)
  * [Incluir uma zona em seu cluster e replicar os nós do trabalhador em seus conjuntos de trabalhadores em múltiplas zonas](#add_zone)
  * [Descontinuado: incluir um nó do trabalhador independente em um cluster](#standalone)

Depois de configurar seu conjunto de trabalhadores, é possível [configurar o escalador automático de cluster](/docs/containers?topic=containers-ca#ca) para incluir ou remover automaticamente nós do trabalhador de seus conjuntos de trabalhadores com base em suas solicitações de recursos de carga de trabalho.
{:tip}

## Incluindo nós do trabalhador redimensionando um conjunto de trabalhadores existente
{: #resize_pool}

É possível incluir ou reduzir o número de nós do trabalhador em seu cluster, redimensionando um conjunto de trabalhadores existente, independentemente de se o conjunto de trabalhadores está em uma zona ou difundido entre múltiplas zonas.
{: shortdesc}

Por exemplo, considere um cluster com um conjunto de trabalhadores que tenha três nós do trabalhador por zona.
* Se o cluster for uma zona única e existir em `dal10`, o conjunto de trabalhadores terá três nós do trabalhador em `dal10`. O cluster tem um total de três nós do trabalhador.
* Se o cluster for de múltiplas zonas e existir em `dal10` e `dal12`, o conjunto de trabalhadores terá três nós do trabalhador em `dal10` e três nós do trabalhador em `dal12`. O cluster terá um total de seis nós do trabalhador.

Para conjuntos de trabalhadores bare metal, tenha em mente que o faturamento é mensal. Se você redimensionar para cima ou para baixo, isso impactará os seus custos para o mês.
{: tip}

Para redimensionar o conjunto de trabalhadores, mude o número de nós do trabalhador que o conjunto de trabalhadores implementa em cada zona:

1. Obtenha o nome do conjunto de trabalhadores que você deseja redimensionar.
    ```
    ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. Redimensione o conjunto de trabalhadores designando o número de nós do trabalhador que você deseja implementar em cada zona. O valor mínimo é 1.
    ```
    ibmcloud oc worker-pool-resize --cluster <cluster_name_or_ID> --worker-pool <pool_name>  --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

3. Verifique se o conjunto de trabalhadores está redimensionado.
    ```
    ibmcloud oc workers --cluster <cluster_name_or_ID> --worker-pool <pool_name>
    ```
    {: pre}

    Saída de exemplo para um conjunto de trabalhadores que está em duas zonas, `dal10` e `dal12`, e é redimensionado para dois nós do trabalhador por zona:
    ```
    ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.8.6_1504
    kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal10   1.8.6_1504
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w9   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.8.6_1504
    kube-dal12-crb20b637238ea471f8d4a8b881aae4962-w10  169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          normal   Ready   dal12   1.8.6_1504
    ```
    {: screen}

## Incluindo nós do trabalhador criando um novo conjunto de trabalhadores
{: #add_pool}

É possível incluir nós do trabalhador em seu cluster, criando um novo conjunto de trabalhadores.
{:shortdesc}

1. Recupere as **Zonas do trabalhador** de seu cluster e escolha a zona na qual você deseja implementar os nós do trabalhador em seu conjunto de trabalhadores. Se você tiver um cluster de zona única, deverá usar a zona que você vê no campo **Zonas do trabalhador**. Para clusters multizona, é possível escolher qualquer uma das **Zonas do trabalhador** existentes de seu cluster ou incluir um dos [locais metro multizona](/docs/containers?topic=containers-regions-and-zones#zones) para a região na qual seu cluster está. É possível listar as zonas disponíveis executando `ibmcloud oc zones`.
   ```
   ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
   ```
   {: pre}

   Saída de exemplo:
   ```
   ...
   Zonas Worker: dal10, dal12, dal13
   ```
   {: screen}

2. Para cada zona, liste as VLANs privadas e públicas disponíveis. Observe a VLAN privada e a VLAN pública que você deseja usar. Se você não tiver uma VLAN privada ou pública, ela será criada automaticamente quando você incluir uma zona em seu conjunto de trabalhadores.
   ```
   ibmcloud oc vlans --zone <zone>
   ```
   {: pre}

3.  Para cada zona, revise os [tipos disponíveis para os nós do trabalhador](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes).

    ```
    ibmcloud oc flavors --zone <zone>
    ```
    {: pre}

4. Crie um conjunto de trabalhadores. Inclua a opção `--label` para rotular automaticamente os nós do trabalhador que estão no conjunto com o rótulo `key=value`. Se você provisionar um conjunto de trabalhadores bare metal, especifique `--hardware dedicated`.
   ```
   ibmcloud oc worker-pool-create --name <pool_name> --cluster <cluster_name_or_ID> --machine-type <flavor> --size-per-zone <number_of_workers_per_zone> --hardware <dedicated_or_shared> --labels <key=value>
   ```
   {: pre}

5. Verifique se o conjunto de trabalhadores foi criado.
   ```
   ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
   ```
   {: pre}

6. Por padrão, incluir um conjunto de trabalhadores cria um conjunto sem zonas. Para implementar os nós do trabalhador em uma zona, deve-se incluir as zonas que você recuperou anteriormente no conjunto de trabalhadores. Se você deseja difundir os nós do trabalhador em múltiplas zonas, repita este comando para cada zona.
   ```
   ibmcloud oc zone-add --zone <zone> --cluster <cluster_name_or_ID> --worker-pools <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
   ```
   {: pre}

7. Verifique se os nós do trabalhador são provisionados na zona que você incluiu. Os nós do trabalhador estão prontos quando o status muda de **provision_pending** para **normal**.
   ```
   ibmcloud oc workers --cluster <cluster_name_or_ID> --worker-pool <pool_name>
   ```
   {: pre}

   Saída de exemplo:
   ```
   ID                                                 Public IP        Private IP      Machine Type      State    Status  Zone    Version
   kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w7   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.8.6_1504
   kube-dal10-crb20b637238ea471f8d4a8b881aae4962-w8   169.xx.xxx.xxx   10.xxx.xx.xxx   b3c.4x16          provision_pending   Ready   dal10   1.8.6_1504
   ```
   {: screen}

## Incluindo nós do trabalhador incluindo uma zona em um conjunto de trabalhadores
{: #add_zone}

É possível estender seu cluster entre múltiplas zonas em uma região incluindo uma zona em seu conjunto de trabalhadores existente.
{:shortdesc}

Quando você inclui uma zona em um conjunto de trabalhadores, os nós do trabalhador que estão definidos em seu conjunto de trabalhadores são provisionados na nova zona e considerados para planejamento futuro de carga de trabalho. O {{site.data.keyword.containerlong_notm}} inclui automaticamente o rótulo `failure-domain.beta.kubernetes.io/region` para a região e o rótulo `failure-domain.beta.kubernetes.io/zone` para a zona em cada nó do trabalhador. O planejador do Kubernetes usa esses rótulos para difundir pods ao longo de zonas dentro da mesma região.

Se você tiver múltiplos conjuntos de trabalhadores em seu cluster, inclua a zona em todos eles para que os nós do trabalhador sejam distribuídos uniformemente em seu cluster.

Antes de iniciar:
*  Para incluir uma zona em seu conjunto de trabalhadores, o conjunto de trabalhadores deve estar em uma [zona com capacidade de múltiplas zonas](/docs/containers?topic=containers-regions-and-zones#zones). Se o seu conjunto de trabalhadores não estiver em uma zona com capacidade de múltiplas zonas, considere [criar um novo conjunto de trabalhadores](#add_pool).
*  Se você tiver múltiplas VLANs para um cluster, múltiplas sub-redes na mesma VLAN ou em um cluster multizona, você deverá ativar um [Virtual Router Function (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) para sua conta de infraestrutura do IBM Cloud para que os nós do trabalhador possam se comunicar entre si na rede privada. Para ativar o VRF, [entre em contato com o seu representante de conta de infraestrutura do IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Para verificar se um VRF já está ativado, use o comando `ibmcloud account show`. Se não for possível ou você não desejar ativar o VRF, ative o [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Para executar essa ação, você precisa da [permissão de infraestrutura](/docs/containers?topic=containers-users#infra_access) **Rede > Gerenciar a rede VLAN Spanning** ou é possível solicitar ao proprietário da conta para ativá-la. Para verificar se a ampliação da VLAN já está ativada, use o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud oc vlan-spanning-get --region <region>`.

Para incluir uma zona com nós do trabalhador em seu conjunto de trabalhadores:

1. Liste as zonas disponíveis e escolha a zona que você deseja incluir em seu conjunto de trabalhadores. A zona que você escolhe deve ser uma zona com capacidade para múltiplas zonas.
   ```
   ibmcloud oc zones
   ```
   {: pre}

2. Listar VLANs disponíveis nessa zona. Se você não tiver uma VLAN privada ou pública, ela será criada automaticamente quando você incluir uma zona em seu conjunto de trabalhadores.
   ```
   ibmcloud oc vlans --zone <zone>
   ```
   {: pre}

3. Liste os conjuntos de trabalhadores em seu cluster e anote seus nomes.
   ```
   ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
   ```
   {: pre}

4. Inclua a zona em seu conjunto de trabalhadores. Se você tiver múltiplos conjuntos de trabalhadores, inclua a zona em todos os seus conjuntos de trabalhadores para que o seu cluster seja balanceado em todas as zonas. Substitua `<pool1_id_or_name,pool2_id_or_name,...>` pelos nomes de todos os seus conjuntos do trabalhador em uma lista separada por vírgula.

    Uma VLAN privada e uma VLAN pública devem existir antes que seja possível incluir uma zona em múltiplos conjuntos de trabalhadores. Se não houver uma VLAN privada e uma pública nessa zona, inclua a zona em um conjunto de trabalhadores primeiro para que uma VLAN privada e uma pública sejam criadas para você. Em seguida, é possível incluir a zona em outros conjuntos de trabalhadores especificando a VLAN privada e a pública que foram criadas para você.
    {: note}

   Se você desejar usar VLANs diferentes para diferentes conjuntos de trabalhadores, repita este comando para cada VLAN e os seus conjuntos de trabalhadores correspondentes. Todos os novos nós do trabalhador são incluídos nas VLANs especificadas, mas as VLANs para quaisquer nós do trabalhador existentes não mudam.
   {: tip}
   ```
   ibmcloud oc zone-add --zone <zone> --cluster <cluster_name_or_ID> --worker-pools <pool1_name,pool2_name,...> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
   ```
   {: pre}

5. Verifique se a zona foi incluída em seu cluster. Procure a zona incluída no campo **Zonas do trabalhador** da saída. Observe que o número total de trabalhadores no campo **Trabalhadores** aumentou porque novos nós do trabalhador são provisionados na zona incluída.
  ```
  ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Saída de exemplo:
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

## Descontinuado: Incluindo nós do trabalhador independentes
{: #standalone}

Se você tem um cluster que foi criado antes de os conjuntos de trabalhadores serem introduzidos, é possível usar os comandos descontinuados para incluir nós do trabalhador independentes.
{: deprecated}

Se você tiver um cluster que foi criado após os conjuntos de trabalhadores serem introduzidos, não será possível incluir nós do trabalhador independentes. Como alternativa, é possível [criar um conjunto de trabalhadores](#add_pool), [redimensionar um conjunto de trabalhadores existente](#resize_pool) ou [incluir uma zona em um conjunto de trabalhadores](#add_zone) para incluir nós do trabalhador em seu cluster.
{: note}

1. Liste as zonas disponíveis e escolha a zona na qual você deseja incluir nós do trabalhador.
   ```
   ibmcloud oc zones
   ```
   {: pre}

2. Liste as VLANs disponíveis nessa zona e anote seus IDs.
   ```
   ibmcloud oc vlans --zone <zone>
   ```
   {: pre}

3. Liste os tipos disponíveis nessa zona.
   ```
   ibmcloud oc flavors --zone <zone>
   ```
   {: pre}

4. Inclua nós do trabalhador independentes no cluster. Para os tipos bare metal, especifique `dedicated`.
   ```
   ibmcloud oc worker-add --cluster <cluster_name_or_ID> --workers <number_of_worker_nodes> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --machine-type <flavor> --hardware <shared_or_dedicated>
   ```
   {: pre}

5. Verifique se os nós do trabalhador estão criados.
   ```
   ibmcloud oc workers --cluster <cluster_name_or_ID>
   ```
   {: pre}

<br />


## Incluindo rótulos em conjuntos de trabalhadores existentes
{: #worker_pool_labels}

É possível designar um conjunto de trabalhadores a um rótulo ao [criar o conjunto de trabalhadores](#add_pool) ou posteriormente seguindo estas etapas. Depois que um conjunto de trabalhadores é rotulado, todos os nós do trabalhador existentes e subsequentes obtêm esse rótulo. Você pode usar rótulos para implementar cargas de trabalho específicas somente para nós do trabalhador no conjunto de trabalhadores, como [nós de borda para o tráfego de rede do balanceador de carga](/docs/containers?topic=containers-edge).
{: shortdesc}

Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1.  Liste os conjuntos de trabalhadores em seu cluster.
    ```
    ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
    ```
    {: pre}
2.  Para rotular o conjunto de trabalhadores com um rótulo `key=value`, use a [API do conjunto de trabalhadores PATCH ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://containers.cloud.ibm.com/global/swagger-global-api/#/clusters/PatchWorkerPool). Formate o corpo da solicitação como no exemplo JSON a seguir.
    ```
    {
      "labels": {"key":"value"},
      "state": "labels"
    }
    ```
    {: codeblock}
3.  Verifique se o conjunto de trabalhadores e o nó do trabalhador têm o rótulo `key=value` que você designou.
    *   Para verificar os conjuntos de trabalhadores:
        ```
        ibmcloud oc worker-pool-get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}
    *   Para verificar os nós do trabalhador:
        1.  Liste os nós do trabalhador no conjunto de trabalhadores e anote o **IP privado**.
            ```
            ibmcloud oc workers --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
            ```
            {: pre}
        2.  Revise o campo **Rótulos** da saída.
            ```
            oc describe node <worker_node_private_IP>
            ```
            {: pre}

Depois de rotular seu conjunto de trabalhadores, é possível usar o [rótulo em suas implementações de app](/docs/containers?topic=containers-app#label) para que suas cargas de trabalho sejam executadas somente nesses nós do trabalhador ou [contaminações ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/) para evitar que as implementações sejam executadas nesses nós do trabalhador.

<br />


## Recuperação automática para seus nós do trabalhador
{: #planning_autorecovery}

Componentes críticos, como `containerd`, `kubelet`, `kube-proxy` e `calico`, devem ser funcionais para ter um nó do trabalhador Kubernetes funcional. Com o tempo, esses componentes podem deixar de funcionar e podem deixar o nó do trabalhador em um estado não funcional. Os nós do trabalhador não funcionais diminuem a capacidade total do cluster e podem resultar em tempo de inatividade para seu app.
{:shortdesc}

É possível [configurar verificações de funcionamento para seu nó do trabalhador e ativar a Recuperação automática](/docs/containers?topic=containers-health#autorecovery). Se a Recuperação automática detecta um nó do trabalhador não funcional com base nas verificações configuradas, a Recuperação automática aciona uma ação corretiva como um recarregamento do S.O. no nó do trabalhador. Para obter mais informações sobre como a Recuperação automática funciona, veja o [blog de Recuperação automática ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2017/12/autorecovery-utilizes-consistent-hashing-high-availability/).



