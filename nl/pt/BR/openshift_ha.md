---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, disaster recovery, dr, ha, hadr

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



# Alta disponibilidade para clusters do OpenShift
{: #ha}

Use os recursos integrados do OpenShift, do Kubernetes e do {{site.data.keyword.containerlong}} para tornar seu cluster do OpenShift mais altamente disponível e para proteger seu app do tempo de inatividade quando um componente em seu cluster falhar.
{: shortdesc}

A alta disponibilidade é uma disciplina principal em uma infraestrutura de TI para manter seus apps funcionando, mesmo após uma falha de site parcial ou integral. O principal propósito de alta disponibilidade é eliminar pontos potenciais de falhas em uma infraestrutura de TI. Por exemplo, é possível se preparar para a falha de um sistema incluindo redundância e configurando mecanismos de failover.

É possível obter alta disponibilidade em diferentes níveis em sua infraestrutura de TI e em diferentes componentes de seu cluster. O nível de disponibilidade que é certo para você depende de vários fatores, como seus requisitos de negócios, os Acordos de Nível de Serviço que você tem com seus clientes e o dinheiro que deseja-se gastar.

## Visão geral de possíveis pontos de falha no Red Hat OpenShift on IBM Cloud
{: #fault_domains}

A arquitetura e a infraestrutura do Red Hat OpenShift on IBM Cloud são projetadas para assegurar a confiabilidade, a baixa latência de processamento e um tempo de inatividade máximo do serviço. No entanto, falhas podem acontecer. Dependendo do serviço hospedado no {{site.data.keyword.cloud_notm}}, você pode não ser capaz de tolerar falhas, mesmo se as falhas duram somente alguns minutos.
{: shortdesc}

O Red Hat OpenShift on IBM Cloud fornece várias abordagens para incluir mais disponibilidade em seu cluster, incluindo redundância e antiafinidade. Revise a imagem a seguir para aprender sobre pontos potenciais de falha e como eliminá-los.

<img src="images/cs_failure_ov.png" alt="Visão geral de domínios de falha em um cluster de alta disponibilidade dentro de uma região do {{site.data.keyword.cloud_notm}}." width="250" style="width:250px; border-style: none"/>

<dl>
<dt> 1. Falha do contêiner ou do pod.</dt>
  <dd><p>Os contêineres e os pods são, pelo design, de curta duração e podem falhar inesperadamente. Por exemplo, um contêiner ou pod pode travar se um erro ocorre em seu app. Para tornar o seu aplicativo altamente disponível, deve-se assegurar de ter instâncias suficientes de seu aplicativo para manipular a carga de trabalho mais instâncias adicionais no caso de uma falha. Idealmente, essas instâncias são distribuídas entre múltiplos nós do trabalhador para proteger o seu app de uma falha do nó do trabalhador.</p>
  <p>Consulte  [ Implementando apps altamente disponíveis ](/docs/containers?topic=containers-app#highly_available_apps).</p></dd>
<dt> 2. Falha do nó do trabalhador.</dt>
  <dd><p>Um nó do trabalhador é uma VM que é executada na parte superior do hardware físico. As falhas do nó do trabalhador incluem indisponibilidades de hardware, como energia, resfriamento ou rede, e problemas na VM em si. É possível considerar uma falha do nó do trabalhador configurando múltiplos nós do trabalhador em seu cluster.</p><p class="note">Os nós do trabalhador em uma zona não têm garantia de estar em hosts de cálculo físico separados. Por exemplo, você pode ter um cluster com três nós do trabalhador, mas todos os três nós do trabalhador foram criados no mesmo host de cálculo físico na zona da IBM. Se este host de cálculo físico fica inativo, todos os nós do trabalhador ficam inativos. Para se proteger contra essa falha, deve-se [configurar um cluster de múltiplas zonas ou criar múltiplos clusters de zona única](/docs/containers?topic=containers-ha_clusters#ha_clusters) em zonas diferentes.</p>
  <p>Consulte [Criando clusters com múltiplos nós do trabalhador.](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_create)</p></dd>
<dt> 3. Falha de cluster.</dt>
  <dd><p>O [Mestre do Kubernetes](/docs/containers?topic=containers-ibm-cloud-kubernetes-service-technology#architecture) é o componente principal que mantém seu cluster funcionando. O mestre armazena recursos de cluster e suas configurações no banco de dados etcd que serve como o ponto único de verdade para seu cluster. O servidor da API do Kubernetes é o ponto de entrada principal para todas as solicitações de gerenciamento de cluster dos nós do trabalhador para o principal ou quando você deseja interagir com os recursos de cluster.<br><br>Se ocorrer uma falha no mestre, suas cargas de trabalho continuarão a serem executadas nos nós do trabalhador, mas não será possível usar comandos `oc` para trabalhar com seus recursos do cluster ou visualizar o funcionamento do cluster até que o servidor da API do Kubernetes no mestre esteja ativo novamente. Se um pod ficar inativo durante a indisponibilidade do mestre, o pod não poderá ser reprogramado até que o nó do trabalhador possa atingir o servidor da API do Kubernetes novamente.<br><br>Durante uma indisponibilidade do mestre, ainda é possível executar comandos `ibmcloud oc` com relação à API do Red Hat OpenShift on IBM Cloud para trabalhar com seus recursos de infraestrutura, como nós do trabalhador ou VLANs. Se você mudar a configuração de cluster atual incluindo ou removendo nós do trabalhador no cluster, suas mudanças não ocorrerão até que o mestre esteja ativo novamente.</p>
  <p class="important">Não reinicie ou reinicialize um nó do trabalhador durante uma indisponibilidade do mestre. Essa ação remove os pods de seu nó do trabalhador. Como o servidor da API do Kubernetes está indisponível, os pods não podem ser reprogramados em outros nós do trabalhador no cluster.</p>
  <p>Os clusters mestres são altamente disponíveis e incluem réplicas para o servidor de API do Kubernetes, o etcd, o planejador e o gerenciador do controlador em hosts separados para proteger contra uma indisponibilidade, como durante uma atualização do mestre.</p><p>Para proteger seu cluster mestre de uma falha de zona, é possível: <ul><li>Crie um cluster em um [local metro multizona](/docs/containers?topic=containers-regions-and-zones#zones) que espalhe o principal entre as zonas.</li><li>configurar um segundo cluster em outra zona.</li></ul></p>
  <p>Consulte  [ Configurando clusters altamente disponíveis. ](/docs/containers?topic=containers-ha_clusters#ha_clusters)</p></dd>
<dt> 4. Falha na zona.</dt>
  <dd><p>Uma falha de zona afeta todos os hosts de cálculo físico e armazenamento NFS. As falhas incluem energia, resfriamento, rede ou indisponibilidades de armazenamento e desastres naturais, como inundações, terremotos e furacões. Para proteger contra uma falha de zona, deve-se ter clusters em duas zonas diferentes que são balanceadas por carga por um balanceador de carga externo.</p>
  <p>Consulte  [ Configurando clusters altamente disponíveis ](/docs/containers?topic=containers-ha_clusters#ha_clusters).</p></dd>    
<dt> 5. Falha de região.</dt>
  <dd><p>Cada região é configurada com um balanceador de carga altamente disponível que seja acessível por meio do terminal de API específico da região. O balanceador de carga roteia as solicitações recebidas e de saída para os clusters nas zonas regionais. A probabilidade de uma falha regional integral é baixa. No entanto, para considerar essa falha, é possível configurar múltiplos clusters em diferentes regiões e conectá-los usando um balanceador de carga externo. Se uma região inteira falhar, o cluster na outra região poderá assumir o controle da carga de trabalho.</p><p class="note">Um cluster de várias regiões requer vários recursos do Cloud e, dependendo de seu app, pode ser complexo e caro. Verifique se você precisa de uma configuração de múltiplas regiões ou se é possível acomodar uma potencial interrupção de serviço. Se você desejar configurar um cluster multiregion, certifique-se de que o seu app e os dados possam ser hospedados em outra região e de que o seu app possa manipular a replicação de dados globais.</p>
  <p>Consulte  [ Configurando clusters altamente disponíveis ](/docs/containers?topic=containers-ha_clusters#ha_clusters).</p></dd>   
<dt> 6a, 6b. Falha de armazenamento.</dt>
  <dd><p>Em um app stateful, os dados têm um papel importante para manter seu app funcionando. Certifique-se de que seus dados estejam altamente disponíveis para que seja possível recuperar-se de uma possível falha. No Red Hat OpenShift on IBM Cloud, é possível escolher entre várias opções para persistir seus dados. Por exemplo, é possível provisionar o armazenamento NFS usando volumes persistentes nativos do Kubernetes ou armazenar seus dados usando um serviço de banco de dados do {{site.data.keyword.cloud_notm}}.</p>
  <p>Consulte  [ Planejando dados altamente disponíveis ](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).</p></dd>
</dl>


