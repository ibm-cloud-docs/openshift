---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, version

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



# Atualizando clusters, nós do trabalhador e componentes do cluster
{: #update}

É possível instalar atualizações para manter seus clusters do {{site.data.keyword.openshiftlong}} atualizados.
{:shortdesc}

## Atualizando o mestre
{: #master}

Periodicamente, o OpenShift libera [atualizações principais, secundárias ou de correção](/docs/openshift?topic=openshift-openshift_versions). As atualizações podem afetar a versão do servidor da API ou outros componentes em seu mestre. A IBM atualiza a versão da correção, mas deve-se atualizar as versões principal e secundária.
{:shortdesc}

**Como faço para saber que preciso atualizar o principal?**</br>
Você é notificado no console e na CLI do {{site.data.keyword.cloud_notm}} quando as atualizações estão disponíveis e também é possível verificar a página [versões suportadas](/docs/openshift?topic=openshift-openshift_versions).

**Os meus nós do trabalhador podem ser executados em uma versão mais recente do que a do principal?**</br>
Os nós do trabalhador não podem executar uma versão do Kubernetes `major.minor` mais recente que o mestre. Primeiro, [atualize seu principal](#update_master) para a versão mais recente do Kubernetes. Em seguida, [atualize os nós do trabalhador](#worker_node) em seu cluster.

Os nós do trabalhador podem executar versões de correção mais recentes do que o mestre, como as versões de correção que são específicas para nós do trabalhador para atualizações de segurança.

**Como as atualizações de correção são aplicadas?**</br>
Por padrão, as atualizações de correção para o mestre são aplicadas automaticamente ao longo do curso de vários dias, portanto, uma versão de correção principal pode ser mostrada como disponível antes de ser aplicada ao seu mestre. A automação de atualização também ignora clusters que estão em um estado não funcional ou têm operações atualmente em andamento. Ocasionalmente, a IBM pode desativar as atualizações automáticas para um fix pack de mestre específico, como uma correção que é necessária somente se um mestre for atualizado de uma versão secundária para outra. Em qualquer um desses casos, é possível [verificar o log de mudanças de versões](/docs/containers?topic=containers-changelog) em busca de qualquer impacto potencial e optar por usar com segurança o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_update) `ibmcloud oc cluster-update` sem esperar que a automação de atualização se aplique.

Diferentemente do mestre, deve-se atualizar seus trabalhadores para cada versão de correção.

**O que acontece durante a atualização do principal?**</br>
Em clusters que executam o Kubernetes versão 1.11 ou mais recente, seu mestre está altamente disponível com três pods do mestre de réplica. Os pods principais têm uma atualização contínua, durante a qual apenas um pod está indisponível por vez. Duas instâncias estão funcionando para que seja possível acessar e mudar o cluster durante a atualização. Os nós do trabalhador, apps e recursos continuam a ser executados.

Para clusters que executam versões anteriores do Kubernetes, quando você atualiza o servidor de API do Kubernetes, o servidor de API fica inativo por cerca de 5 a 10 minutos. Durante a atualização, não é possível acessar nem mudar o cluster. No entanto, os nós do trabalhador, apps e recursos que os usuários do cluster implementaram não são modificados e continuam a ser executados.

**Posso recuperar a atualização?**</br>
Não, não é possível retroceder um cluster para uma versão anterior depois que o processo de atualização ocorre. Certifique-se de usar um cluster de teste e siga as instruções para tratar de problemas potenciais antes de atualizar seu principal de produção.

**Qual processo posso seguir para atualizar o principal?**</br>
O diagrama a seguir mostra o processo que você pode usar para atualizar seu mestre.

![Melhor prática de atualização de mestre](/images/update-tree.png)

Figura 1. Atualizando o diagrama do processo de mestre do Kubernetes

{: #update_master}
Antes de iniciar, certifique-se de que tenha a função da plataforma [**Operador** ou **Administrador** do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-users#platform).

Para atualizar a versão _principal_ ou _secundária_ do mestre do Kubernetes:

1.  Revise as [mudanças do Kubernetes](/docs/containers?topic=containers-cs_versions) e faça as atualizações marcadas como _Atualizar antes do mestre_.

2.  Atualize o servidor da API e os componentes principais associados usando o [console do {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/login) ou executando o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_update) `ibmcloud oc cluster-update` da CLI.

3.  Aguarde alguns minutos e, em seguida, confirme se a atualização está concluída. Revise a versão do servidor da API no painel de clusters do {{site.data.keyword.cloud_notm}} ou execute `ibmcloud oc clusters`.

4.  Instale a versão do [`oc cli`](/docs/containers?topic=containers-cs_cli_install#kubectl) que corresponde à versão do servidor da API que é executada no mestre. [O Kubernetes não suporta ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/setup/version-skew-policy/) versões de cliente `oc` com diferença de duas ou mais versões da versão do servidor (n +/- 2).

Quando a atualização do mestre estiver concluída, será possível atualizar os nós do trabalhador.

<br />


## Atualizando nós do trabalhador
{: #worker_node}

Você recebeu uma notificação para atualizar seus nós do trabalhador. O que isso significa? Como as atualizações de segurança e as correções são colocadas no lugar para o servidor de API e outros componentes principais, deve-se ter certeza de que os nós do trabalhador permaneçam sincronizados.
{: shortdesc}

**O que acontece com meus aplicativos durante uma atualização?**</br>
Se executar apps como parte de uma implementação em nós do trabalhador que você atualizar, os apps serão reprogramados em outros nós do trabalhador no cluster. Esses nós do trabalhador podem estar em um conjunto de trabalhadores diferente ou, se você tiver nós do trabalhador independentes, os apps poderão estar planejados em nós do trabalhador independentes. Para evitar tempo de inatividade para seu app, deve-se assegurar que você tenha capacidade suficiente no cluster para transportar a carga de trabalho.

**Como posso controlar quantos nós do trabalhador ficam inativos de cada vez durante a atualização?**</br>
Se você precisar que todos os nós do trabalhador estejam funcionando, considere [redimensionar seu conjunto de trabalhadores](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_pool_resize) ou [incluir nós do trabalhador independentes](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_add) para incluir mais nós do trabalhador. Será possível remover os nós do trabalhador adicionais depois que a atualização for concluída.

Além disso, é possível criar um mapa de configuração do Kubernetes que especifique o número máximo de nós do trabalhador que podem ficar indisponíveis em um horário durante a atualização. Os nós do trabalhador são identificados pelos rótulos de nó do trabalhador. É possível usar rótulos fornecidos pela IBM ou rótulos customizados que você incluiu no nó do trabalhador.

**E se eu escolher não definir um mapa de configuração?**</br>
Quando o mapa de configuração não está definido, o padrão é usado. Por padrão, um máximo de 20% de todos os nós do trabalhador em cada cluster pode ficar indisponível durante o processo de atualização.

** Antes de iniciar **:
- [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
- [Atualizar o mestre](#master). A versão do nó do trabalhador não pode ser maior que a versão do servidor de API que é executada em seu mestre do Kubernetes.
- Faça todas as mudanças marcadas com _Atualizar após o mestre_ nos guias de preparação da versão dos [clusters Kubernetes](/docs/containers?topic=containers-cs_versions) ou dos [clusters OpenShift](/docs/openshift?topic=openshift-openshift_versions).
- Se desejar aplicar uma atualização de correção, revise o log de mudanças dos [clusters Kubernetes](/docs/containers?topic=containers-changelog#changelog) ou dos [clusters OpenShift](/docs/openshift?topic=openshift-openshift_versions).
- Certifique-se de que você tenha a função da plataforma [**Operador** ou **Administrador** do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-users#platform). </br>

As atualizações para os nós do trabalhador podem causar tempo de inatividade para seus apps e serviços. A máquina do nó do trabalhador tem a imagem reinstalada, e os dados são excluídos se não [armazenados fora do pod](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).
{: important}

{: #worker-up-configmap}
**Para criar um mapa de configuração e atualizar nós do trabalhador**:

1.  Liste os nós do trabalhador disponíveis e anote o seu endereço IP privado.

    ```
    ibmcloud oc workers --cluster <cluster_name_or_ID>
    ```
    {: pre}

2. Visualizar os rótulos de um nó do trabalhador. É possível localizar os rótulos de nó do trabalhador na seção **Rótulos** de sua saída da CLI. Cada rótulo consiste em um `NodeSelectorKey` e um `NodeSelectorValue`.
   ```
   oc describe node <private_worker_IP>
   ```
   {: pre}

   Saída de exemplo:
   ```
   Name:               10.184.58.3
   Roles:              <none>
   Labels:             arch=amd64
                    beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    failure-domain.beta.kubernetes.io/region=us-south
                    failure-domain.beta.kubernetes.io/zone=dal12
                    ibm-cloud.kubernetes.io/encrypted-docker-data=true
                    ibm-cloud.kubernetes.io/iaas-provider=softlayer
                    ibm-cloud.kubernetes.io/machine-type=u3c.2x4.encrypted
                    kubernetes.io/hostname=10.123.45.3
                    privateVLAN=2299001
                    publicVLAN=2299012
   Annotations:        node.alpha.kubernetes.io/ttl=0
                    volumes.kubernetes.io/controller-managed-attach-detach=true
   CreationTimestamp:  Tue, 03 Apr 2018 15:26:17 -0400
   Taints:             <none>
   Unschedulable:      false
   ```
   {: screen}

3. Crie um mapa de configuração e defina as regras de indisponibilidade para seus nós do trabalhador. O exemplo a seguir mostra quatro verificações, o `zonecheck.json`, `regioncheck.json`, `defaultcheck.json` e um modelo de verificação. É possível usar essas verificações de exemplo para definir regras para nós do trabalhador em uma zona específica (`zonecheck.json`), região (`regioncheck.json`) ou para todos os nós do trabalhador que não correspondem a nenhuma das verificações definidas no mapa de configuração (` defaultcheck.json`). Use o modelo de verificação para criar sua própria verificação. Para cada verificação, para identificar um nó do trabalhador, deve-se escolher um dos rótulos de nó do trabalhador que você recuperou na etapa anterior.  

   Para cada verificação, é possível configurar somente um valor para <code>NodeSelectorKey</code> e <code>NodeSelectorValue</code>. Se você desejar configurar regras para mais de uma região, zona ou outros rótulos de nó do trabalhador, crie uma nova verificação. Defina até 10 verificações em um mapa de configuração. Se você incluir mais verificações, elas serão ignoradas.
   {: note}

   Exemplo:
   ```
   apiVersion: v1
    kind: ConfigMap
    metadata:
      name: ibm-cluster-update-configuration
      namespace: kube-system
    data:
     drain_timeout_seconds: "120"
     zonecheck.json: |
       {
        "MaxUnavailablePercentage": 30,
        "NodeSelectorKey": "failure-domain.beta.kubernetes.io/zone",
        "NodeSelectorValue": "dal13"
      }
    regioncheck.json: |
       {
        "MaxUnavailablePercentage": 20,
        "NodeSelectorKey": "failure-domain.beta.kubernetes.io/region",
        "NodeSelectorValue": "us-south"
      }
    defaultcheck.json: |
       {
        "MaxUnavailablePercentage": 20
      }
    <check_name>: |
      {
        "MaxUnavailablePercentage": <value_in_percentage>,
        "NodeSelectorKey": "<node_selector_key>",
        "NodeSelectorValue": "<node_selector_value>"
      }
   ```
   {: codeblock}

   <table summary="A primeira linha na tabela abrange ambas as colunas. O resto das linhas deve ser lido da esquerda para a direita, com o parâmetro na coluna um e a descrição que corresponde na coluna dois.">
   <caption>Componentes ConfigMap</caption>
    <thead>
      <th colspan=2><img src="images/idea.png" alt="Ícone de ideia"/> Entendendo os componentes </th>
    </thead>
    <tbody>
      <tr>
        <td><code>drain_timeout_seconds</code></td>
        <td> Opcional: o tempo limite em segundos para aguardar o [dreno ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/) ser concluído. A drenagem de um nó do trabalhador remove com segurança todos os pods existentes do nó do trabalhador e reagenda os pods em outros nós do trabalhador no cluster. Os valores aceitos são números inteiros no intervalo de 1 a 180. O valor padrão é 30.</td>
      </tr>
      <tr>
        <td><code>zonecheck.json</code></br><code>regioncheck.json</code></td>
        <td>Duas verificações que definem uma regra para um conjunto de nós do trabalhador que é possível identificar com o <code>NodeSelectorKey</code> e o <code>NodeSelectorValue</code> especificados. O <code>zonecheck.json</code> identifica os nós do trabalhador com base em seu rótulo de zona e o <code>regioncheck.json</code> usa o rótulo de região que é incluído em cada nó do trabalhador durante o fornecimento. No exemplo, 30% de todos os nós do trabalhador que têm <code>dal13</code> como seu rótulo de zona e 20% de todos os nós do trabalhador em <code>us-south</code> podem ficar indisponíveis durante a atualização.</td>
      </tr>
      <tr>
        <td><code>defaultcheck.json</code></td>
        <td>Se você não criar um mapa de configuração ou o mapa estiver configurado incorretamente, o padrão do Kubernetes será aplicado. Por padrão, somente 20% dos nós do trabalhador no cluster podem estar indisponíveis de cada vez. É possível substituir o valor padrão, incluindo a verificação padrão em seu mapa de configuração. No exemplo, cada nó do trabalhador que não é especificado nas verificações de zona e região (<code>dal13</code> ou <code>us-south</code>) pode estar indisponível durante a atualização. </td>
      </tr>
      <tr>
        <td><code>MaxUnavailablePercentage</code></td>
        <td>O número máximo de nós que podem ficar indisponíveis para uma chave e um valor de rótulo especificados, que são especificados como uma porcentagem. Um nó do trabalhador está indisponível durante o processo de implementação, recarregamento ou provisionamento. Os nós do trabalhador enfileirados são bloqueados de atualização se excedem qualquer porcentagem máxima indisponível definida. </td>
      </tr>
      <tr>
        <td><code>NodeSelectorKey</code></td>
        <td>A chave de rótulo do nó do trabalhador para o qual você deseja configurar uma regra. É possível configurar regras para os rótulos padrão que são fornecidos pela IBM, bem como nos rótulos de nó do trabalhador que você criou. <ul><li>Se você deseja incluir uma regra para nós do trabalhador que pertencem a um conjunto de trabalhadores, é possível usar o rótulo <code>ibm-cloud.kubernetes.io/machine-type</code>. </li><li> Se você tiver mais de um conjunto de trabalhadores com o mesmo tipo de máquina, use um rótulo customizado. </li></ul></td>
      </tr>
      <tr>
        <td><code>NodeSelectorValue</code></td>
        <td>O valor do rótulo que o nó do trabalhador deve ter para ser considerado para a regra que você define. </td>
      </tr>
    </tbody>
   </table>

4. Crie o mapa de configuração em seu cluster.
   ```
   oc apply -f <filepath/configmap.yaml>
   ```
   {: pre}

5.  Verifique se o mapa de configuração foi criado.
    ```
    oc get configmap --namespace kube-system
    ```
    {: pre}

6.  Atualize os nós do trabalhador.

    ```
    ibmcloud oc worker-update --cluster <cluster_name_or_ID> --workers <worker_node1_ID> <worker_node2_ID>
    ```
    {: pre}

7. Opcional: verifique os eventos que são acionados pelo mapa de configuração e quaisquer erros de validação que ocorrem. Os eventos podem ser revisados na seção **Eventos** de sua saída da CLI.
   ```
   oc describe -n kube-system cm ibm-cluster-update-configuration
   ```
   {: pre}

8. Confirme se a atualização está concluída, revisando a versão do Kubernetes de seus nós do trabalhador.  
   ```
   oc get nodes
   ```
   {: pre}

9. Verifique se você não tem nós do trabalhador duplicados. Em alguns casos, clusters mais velhos podem listar nós do trabalhador duplicados com um status de **`NotReady`** após uma atualização. Para remover duplicatas, consulte [Resolução de problemas](/docs/containers?topic=containers-cs_troubleshoot_clusters#cs_duplicate_nodes).

Próximas etapas:
-   Repita o processo de atualização com outros conjuntos de trabalhadores.
-   Informe os desenvolvedores que trabalham no cluster para atualizar sua CLI `oc` para a versão do mestre do Kubernetes.
-   Se o painel do Kubernetes não exibir os gráficos de utilização, [exclua o pod `kube-dashboard`](/docs/containers?topic=containers-cs_troubleshoot_health#cs_dashboard_graphs).


### Atualizando nós do trabalhador no console
{: #worker_up_console}

Depois de configurar o mapa de configuração pela primeira vez, é possível, então, atualizar os nós do trabalhador usando o console do {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Antes de iniciar:
- [Configure um configmap](#worker_node) para controlar como os nós do trabalhador são atualizados.
- [Atualizar o mestre](#master). A versão do nó do trabalhador não pode ser maior que a versão do servidor de API que é executada em seu mestre do Kubernetes.
- Faça todas as mudanças marcadas com _Atualizar após o mestre_ nos guias de preparação da versão dos [clusters Kubernetes](/docs/containers?topic=containers-cs_versions) ou dos [clusters OpenShift](/docs/openshift?topic=openshift-openshift_versions).
- Se desejar aplicar uma atualização de correção, revise o log de mudanças dos [clusters Kubernetes](/docs/containers?topic=containers-changelog#changelog) ou dos [clusters OpenShift](/docs/openshift?topic=openshift-openshift_versions).
- Certifique-se de que você tenha a função da plataforma [**Operador** ou **Administrador** do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-users#platform). </br>

As atualizações para os nós do trabalhador podem causar tempo de inatividade para seus apps e serviços. A máquina do nó do trabalhador tem a imagem reinstalada, e os dados são excluídos se não [armazenados fora do pod](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).
{: important}

Para atualizar os nós do trabalhador por meio do console:
1.  No menu do [console do {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/) ![Ícone de menu](../icons/icon_hamburger.svg "Ícone de menu"), clique em **Kubernetes**.
2.  Na página **Clusters**, clique em seu cluster.
3.  Na guia **Nós do trabalhador**, selecione a caixa de seleção para cada nó do trabalhador que você deseja atualizar. Uma barra de ação é exibida sobre a linha de cabeçalho da tabela.
4.  Na barra de ação, clique em **Atualizar**.

<br />



## Atualizando tipos (tipos de máquina)
{: #machine_type}

É possível atualizar os tipos, ou tipos de máquina, de seus nós do trabalhador, incluindo novos nós do trabalhador e removendo os antigos. Por exemplo, se o seu cluster tiver descontinuado os tipos de nó de trabalhador `x1c` ou `x2c` do Ubuntu 16 mais antigo, crie nós do trabalhador do Ubuntu 18 que usam tipos com `x3c` nos nomes.
{: shortdesc}

Antes de iniciar:
- [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
- Se você armazenar dados em seu nó do trabalhador, os dados serão excluídos se não [armazenados fora do nó do trabalhador](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).
- Certifique-se de que você tenha a função da plataforma [**Operador** ou **Administrador** do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-users#platform).

Para atualizar os tipos:

1. Liste os nós do trabalhador disponíveis e anote o seu endereço IP privado.
   - **Para nós do trabalhador em um conjunto de trabalhadores**:
     1. Liste os conjuntos de trabalhadores disponíveis em seu cluster.
        ```
        ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
        ```
        {: pre}

     2. Liste os nós do trabalhador no conjunto de trabalhadores. Observe o **ID** e o **IP privado**.
        ```
        ibmcloud oc workers --cluster <cluster_name_or_ID> --worker-pool <pool_name>
        ```
        {: pre}

     3. Obtenha os detalhes para um nó do trabalhador e anote a zona, o ID de VLAN privada e pública.
        ```
        ibmcloud oc worker-get --cluster <cluster_name_or_ID> --worker <worker_ID>
        ```
        {: pre}

   - **Descontinuado: para nós do trabalhador independentes**:
     1. Liste os nós do trabalhador disponíveis. Observe o **ID** e o **IP privado**.
        ```
        ibmcloud oc workers --cluster <cluster_name_or_ID>
        ```
        {: pre}

     2. Obtenha os detalhes para um nó do trabalhador e anote a zona, o ID da VLAN privada e o ID da VLAN pública.
        ```
        ibmcloud oc worker-get --cluster <cluster_name_or_ID> --worker <worker_ID>
        ```
        {: pre}

2. Liste os tipos disponíveis na zona.
   ```
   ibmcloud oc flavors --zone <zone>
   ```
   {: pre}

3. Crie um nó do trabalhador com o novo tipo de máquina.
   - **Para nós do trabalhador em um conjunto de trabalhadores**:
     1. Crie um conjunto de trabalhadores com o número de nós do trabalhador que você deseja substituir.
        ```
        ibmcloud oc worker-pool-create --name <pool_name> --cluster <cluster_name_or_ID> --machine-type <flavor> --size-per-zone <number_of_workers_per_zone>
        ```
        {: pre}

     2. Verifique se o conjunto de trabalhadores foi criado.
        ```
        ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
        ```
        {: pre}

     3. Inclua a zona em seu conjunto de trabalhadores que você recuperou anteriormente. Ao incluir uma zona, os nós do trabalhador que estão definidos em seu conjunto de trabalhadores são provisionados na zona e considerados para planejamento futuro de carga de trabalho. Se você desejar difundir os nós do trabalhador em múltiplas zonas, escolha uma [zona com capacidade para múltiplas zonas](/docs/containers?topic=containers-regions-and-zones#zones).
        ```
        ibmcloud oc zone-add --zone <zone> --cluster <cluster_name_or_ID> --worker-pools <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
        ```
        {: pre}

   - **Descontinuado: para nós do trabalhador independentes**:
       ```
       ibmcloud oc worker-add --cluster <cluster_name> --machine-type <flavor> --workers <number_of_worker_nodes> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
       ```
       {: pre}

4. Aguarde até que os nós do trabalhador sejam implementados. Quando o estado do nó do trabalhador muda para **Normal**, a implementação está concluída.
   ```
   ibmcloud oc workers --cluster <cluster_name_or_ID>
   ```
   {: pre}
5.  Para evitar o tempo de inatividade, reagende os aplicativos dos nós do trabalhador antigos antes de excluir os nós do trabalhador antigos.
    1.  Marque o nó do trabalhador como não programável em um processo conhecido como bloqueio. Ao bloquear um nó do trabalhador, ele fica indisponível para planejamento futuro do pod. Use o **IP privado** do nó do trabalhador que você recuperou anteriormente, que é o nome do nó do trabalhador no Kubernetes.
        ```
        oc cordon <private_IP_address_of_worker_node>
        ```
        {: pre}
    2.  Verifique se o planejamento do pod está desativado para o nó do trabalhador verificando se o status é **SchedulingDisabled**.
        ```
        oc get nodes
        ```
        {: pre}
    3.  Force os pods para que sejam removidos do nó do trabalhador e reprogramados nos nós do trabalhador restantes no cluster. Esse processo pode levar alguns minutos.
        ```
        oc drain <worker_name>
        ```
        {: pre}
6. Remova o nó do trabalhador antigo. **Nota**: se você estiver removendo um tipo que é faturado mensalmente (como bare metal), você será cobrado pelo mês inteiro.
   - **Para nós do trabalhador em um conjunto de trabalhadores**:
     1. Remova o conjunto de trabalhadores com o tipo de máquina antigo. A remoção de um conjunto de trabalhadores remove todos os nós do trabalhador no conjunto em todas as zonas. Esse processo pode levar alguns minutos para ser concluído.
        ```
        ibmcloud oc worker-pool-rm --worker-pool <pool_name> --cluster <cluster_name_or_ID>
        ```
        {: pre}

     2. Verifique se o conjunto de trabalhadores foi removido.
        ```
        ibmcloud oc worker-pools --cluster <cluster_name_or_ID>
        ```
        {: pre}

   - **Descontinuado: para nós do trabalhador independentes**:
      ```
      ibmcloud oc worker-rm --cluster <cluster_name> --worker <worker_node>
      ```
      {: pre}

7. Verifique se os nós do trabalhador foram removidos de seu cluster.
   ```
   ibmcloud oc workers --cluster <cluster_name_or_ID>
   ```
   {: pre}

8. Repita essas etapas para atualizar outros conjuntos de trabalhadores ou nós do trabalhador independentes para diferentes tipos.

## Atualizando componentes do cluster
{: #components}

Seu cluster do {{site.data.keyword.containerlong_notm}} é fornecido com componentes, como o Fluentd para a criação de log, que são instalados automaticamente quando você provisiona o cluster. Por padrão, esses componentes são atualizados automaticamente pela IBM. No entanto, é possível desativar as atualizações automáticas para alguns componentes e atualizá-las manualmente separadamente dos nós principal e do trabalhador.
{: shortdesc}

**Quais componentes padrão eu posso atualizar separadamente do cluster?**</br>
Opcionalmente, é possível desativar atualizações automáticas para os componentes a seguir:
* [ Fluentd para criação de log ](#logging-up)
* [Balanceador de carga do aplicativo Ingress (ALB)](#alb)

**Há componentes que eu não posso atualizar separadamente do cluster?**</br>

Sim. Seu cluster é implementado com os componentes gerenciados e recursos associados a seguir que não podem ser mudados, exceto para escalar pods ou editar configmaps para obter determinados benefícios de desempenho. Se você tentar mudar um desses componentes de implementação, suas configurações originais serão restauradas em um intervalo regular.

* `coredns`
* `coredns-autoscaler`
* `heapster`
* `ibm-file-plugin`
* ` ibm-storage-watcher `
* ` ibm-keepalived-watcher `
* ` kube-dns-amd64 `
* ` kube-dns-autoscaler `
* `kubernetes-painel`
* `metrics-server`
* ` vpn `

É possível visualizar esses recursos usando o rótulo `addonmanager.kubernetes.io/mode: Reconcile`. Por exemplo:

```
oc get deployments --all-namespaces -l addonmanager.kubernetes.io/mode=Reconcile
```
{: pre}

**Posso instalar outros plug-ins ou complementos além dos componentes padrão?**</br>
Sim. O {{site.data.keyword.containerlong_notm}} fornece outros plug-ins e complementos que você pode escolher para incluir recursos em seu cluster. Por exemplo, você pode desejar [usar gráficos do Helm](/docs/containers?topic=containers-helm#public_helm_install) para instalar o [plug-in de armazenamento de bloco](/docs/containers?topic=containers-block_storage#install_block) ou [VPN do strongSwan](/docs/containers?topic=containers-vpn#vpn-setup). Ou, talvez você deseje ativar os complementos gerenciados pela IBM em seu cluster, como [Istio](/docs/containers?topic=containers-istio) ou [Knative](/docs/containers?topic=containers-serverless-apps-knative). Deve-se atualizar esses gráficos e complementos do Helm separadamente seguindo as instruções nos arquivos leia-me do gráfico do Helm ou seguindo as etapas para [atualizar complementos gerenciados](/docs/containers?topic=containers-managed-addons#updating-managed-add-ons).

### Gerenciando atualizações automáticas para Fluentd
{: #logging-up}

Para mudar as configurações de criação de log ou de filtro, o componente Fluentd deve estar na versão mais recente. Por padrão, as atualizações automáticas para o componente são ativadas.
{: shortdesc}

É possível gerenciar atualizações automáticas do componente Fluentd das maneiras a seguir. **Nota**: para executar os comandos a seguir, deve-se ter a função da plataforma [**Administrador** do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-users#platform) para o cluster.

* Verifique se as atualizações automáticas estão ativadas executando o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_log_autoupdate_get) `ibmcloud oc logging-autoupdate-get --cluster <cluster_name_or_ID>`.
* Desative as atualizações automáticas executando o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_log_autoupdate_disable) `ibmcloud oc logging-autoupdate-disable`.
* Se as atualizações automáticas estiverem desativadas, mas for necessário mudar sua configuração, você terá duas opções:
    * Ativar as atualizações automáticas para os seus pods do Fluentd.
        ```
        ibmcloud oc logging-autoupdate-enable --cluster <cluster_name_or_ID>
        ```
        {: pre}
    * Forçar uma atualização única quando usar um comando de criação de log que inclua a opção `--force-update`. **Nota**: seus pods são atualizados para a versão mais recente do componente Fluentd, mas o Fluentd não é atualizado automaticamente a partir de agora.
        Exemplo de comando:

        ```
        ibmcloud oc logging-config-update --cluster <cluster_name_or_ID> --id <log_config_ID> --type <log_type> --force-update
        ```
        {: pre}

### Gerenciando atualizações automáticas para ALBs do Ingress
{: #alb}

Controle quando o componente do balanceador de carga do aplicativo (ALB) do Ingress é atualizado.
{: shortdesc}

Quando o componente ALB do Ingress é atualizado, os contêineres `nginx-ingress` e `ingress-auth` em todos os pods do ALB são atualizados para a versão de construção mais recente. Por padrão, as atualizações automáticas para ALBs são ativadas. As atualizações são executadas continuamente para que os ALBs do Ingress não experimentem nenhum tempo de inatividade. Quando um pod reinicia após a aplicação da atualização, uma [verificação de prontidão](/docs/containers?topic=containers-ingress-settings#readiness-check) evita que o pod do ALB tente rotear as solicitações de tráfego até que todos os arquivos de recursos do Ingress sejam analisados. Essa verificação de prontidão evita a perda de solicitação durante as atualizações do pod do ALB e pode levar até 5 minutos.

Se desativar as atualizações automáticas, você será responsável por atualizar seus ALBs. Conforme as atualizações se tornam disponíveis, você é notificado na CLI quando executa os comandos `ibmcloud oc albs` ou `alb-autoupdate-get`.

Quando você atualiza a versão principal ou secundária do Kubernetes do seu cluster, a IBM faz as mudanças necessárias automaticamente na implementação do Ingress, mas não muda a versão de construção de seus ALBs do Ingress. Você é responsável por verificar a compatibilidade das versões mais recentes do Kubernetes e das imagens de seus ALBs do Ingress.
{: note}

Antes de iniciar:

1. Verifique se os ALBs estão em execução.
    ```
    ibmcloud oc albs
    ```
    {: pre}

2. Verifique o status de atualizações automáticas para o componente ALB do Ingress.
    ```
    ibmcloud oc alb-autoupdate-get --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Saída de exemplo quando atualizações automáticas são ativadas:
    ```
    Retrieving automatic update status of application load balancer (ALB) pods in cluster mycluster...
    OK
    Automatic updates of the ALB pods are enabled in cluster mycluster
    ALBs are at the latest version in cluster mycluster
    ```
    {: screen}

    Saída de exemplo quando atualizações automáticas são desativadas:
    ```
    Retrieving automatic update status of application load balancer (ALB) pods in cluster mycluster...
    OK
    Automatic updates of the ALB pods are disabled in cluster mycluster
    ALBs are not at the latest version in cluster mycluster. Para visualizar a versão atual, execute 'ibmcloud oc albs'.
    ```
    {: screen}

3. Verifique a versão atual de **Construção** de seus pods do ALB.
    ```
    ibmcloud oc albs --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Saída de exemplo:
    ```
    ALB ID                                            Enabled   Status     Type      ALB IP          Zone    Build                           ALB VLAN ID
    private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   10.xxx.xx.xxx   dal10   ingress:411/ingress-auth:315*   2234947
    public-crdf253b6025d64944ab99ed63bb4567b6-alb2    true      enabled    public    169.xx.xxx.xxx  dal10   ingress:411/ingress-auth:315*   2234945

    * Uma atualização está disponível para os pods do ALB. Revise quaisquer mudanças potencialmente disruptivas para a versão mais recente antes de atualizar: https://cloud.ibm.com/docs/containers?topic=containers-update#alb
    ```
    {: screen}

É possível gerenciar atualizações automáticas do componente ALB do Ingress das maneiras a seguir. **Nota**: para executar os comandos a seguir, deve-se ter a função da plataforma [**Editor** ou **Administrador** do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-users#platform) para o cluster.
* Desative as atualizações automáticas.
    ```
    ibmcloud oc alb-autoupdate-disable --cluster <cluster_name_or_ID>
    ```
    {: pre}
* Atualize manualmente seus ALBs do Ingress.
    1. Se uma atualização estiver disponível e você desejar atualizar seus ALBs, primeiro verifique o [log de mudanças para obter a versão mais recente do componente ALB do Ingress](/docs/containers?topic=containers-cluster-add-ons-changelog#alb_changelog) para verificar quaisquer mudanças potencialmente disruptivas.
    2. Force uma atualização única de seus pods do ALB. Todos os pods do ALB no cluster são atualizados para a versão de construção mais recente. Não é possível atualizar um ALB individual ou escolher para qual construção atualizar os ALBs. As atualizações automáticas permanecem desativadas.
        ```
        ibmcloud oc alb-update --cluster <cluster_name_or_ID>
        ```
        {: pre}
* Se os pods do ALB foram atualizados recentemente, mas uma configuração customizada para seus ALBs foi afetada pela construção mais recente, será possível recuperar a atualização para a construção em que os pods do ALB estavam em execução anteriormente. **Nota**: depois de retroceder uma atualização, as atualizações automáticas para os pods do ALB são desativadas.
    ```
    ibmcloud oc alb-rollback --cluster <cluster_name_or_ID>
    ```
    {: pre}
* Reative as atualizações automáticas. Sempre que a próxima construção se torna disponível, os pods do ALB são atualizados automaticamente para a construção mais recente.
    ```
    ibmcloud oc alb-autoupdate-enable --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />


## Atualizando complementos gerenciados
{: #addons}

Os complementos {{site.data.keyword.containerlong_notm}} gerenciados são uma maneira fácil de aprimorar seu cluster com recursos de software livre, como Istio ou Knative. A versão da ferramenta de software livre incluída em seu cluster é testada pela IBM e aprovada para ser usada no {{site.data.keyword.containerlong_notm}}. Para atualizar complementos gerenciados que você ativou em seu cluster para as versões mais recentes, consulte [Atualizando complementos gerenciados](/docs/containers?topic=containers-managed-addons#updating-managed-add-ons).


