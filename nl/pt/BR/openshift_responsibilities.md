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


# Suas responsabilidades usando o Red Hat OpenShift on IBM Cloud
{: #responsibilities_openshift}

Aprenda sobre responsabilidades, termos e condições que você tem quando usa o {{site.data.keyword.containerlong}} para provisionar clusters do Red Hat OpenShift on IBM Cloud.
{:shortdesc}

## Responsabilidades de gerenciamento de cluster
{: #responsibilities}

A IBM fornece uma plataforma de nuvem corporativa para a implementação de aplicativos com os serviços do {{site.data.keyword.cloud_notm}} DevOps, de IA, de dados e de segurança. Você escolhe como configurar, integrar e operar seus aplicativos e serviços na nuvem.
{:shortdesc}

<table summary="A tabela mostra as suas responsabilidades e as da IBM. As linhas devem ser lidas da esquerda para a direita, com os ícones representando cada responsabilidade na coluna um e a descrição na coluna dois.">
<caption>Suas responsabilidades e da IBM</caption>
  <thead>
  <th colspan=2>Responsabilidades por tipo</th>
  </thead>
  <tbody>
    <tr>
    <td align="center"><img src="images/icon_clouddownload.svg" alt="Ícone de uma nuvem com uma seta apontando para baixo"/><br>Infraestrutura em nuvem</td>
    <td>
    **Responsabilidades da IBM**:
    <ul><li>Implemente um principal dedicado e totalmente gerenciado e disponível em uma conta segura de uma infraestrutura da IBM para cada cluster.</li>
    <li>Provisione nós do trabalhador em sua conta de infraestrutura do IBM Cloud.</li>
    <li>Configure os componentes de gerenciamento de cluster, como VLANs e balanceadores de carga.</li>
    <li>Atenda a solicitações de mais infraestrutura, como a inclusão e a remoção de nós do trabalhador, a criação de sub-redes padrão e o fornecimento de volumes de armazenamento em resposta a solicitações de volume persistente.</li>
    <li>Integre recursos de infraestrutura ordenados para trabalhar automaticamente com sua arquitetura de cluster e se tornar disponíveis para seus aplicativos e cargas de trabalho implementados.</li></ul>
    <br><br>
    **As suas responsabilidades**:
    <ul><li>Use as ferramentas de API, CLI ou console fornecidas para ajustar a capacidade de [cálculo](/docs/containers?topic=containers-clusters#clusters) e de [armazenamento](/docs/containers?topic=containers-storage_planning#storage_planning) e a [configuração de rede](/docs/containers?topic=containers-cs_network_cluster#cs_network_cluster) para atender às necessidades de sua carga de trabalho.</li></ul><br><br>
    </td>
     </tr>
     <tr>
     <td align="center"><img src="images/icon_tools.svg" alt="Ícone de uma chave"/><br>Cluster gerenciado</td>
     <td>
     **Responsabilidades da IBM**:
     <ul><li>Forneça um conjunto de ferramentas para automatizar o gerenciamento de cluster, como a [API ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://containers.cloud.ibm.com/global/swagger-global-api/), o [plug-in da CLI](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli) e o [console ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/kubernetes/clusters) do Red Hat OpenShift on IBM Cloud.</li>
     <li>Aplique automaticamente atualizações de correção de S.O., segurança e versão do principal do Kubernetes. Disponibilize atualizações principais e secundárias para a aplicação.</li>
     <li>Atualize e recupere componentes operacionais do Red Hat OpenShift on IBM Cloud e do Kubernetes dentro do cluster, como o balanceador de carga do aplicativo Ingress e o plug-in de armazenamento de arquivos.</li>
     <li>Faça backup e recupere dados em etcd, como seus arquivos de configuração de carga de trabalho do Kubernetes</li>
     <li>Configure uma conexão OpenVPN entre os nós principal e do trabalhador quando o cluster for criado.</li>
     <li>Monitore e relate o funcionamento dos nós principal e do trabalhador nas diversas interfaces.</li>
     <li>Forneça atualizações de correção, principais e secundárias de S.O., segurança e versão do trabalhador.</li>
     <li>Atenda às solicitações de automação para atualizar e recuperar nós do trabalhador. Forneça a [Recuperação automática do nó do trabalhador](/docs/containers?topic=containers-health#autorecovery) opcional.</li>
     <li>Forneça ferramentas, como o [dimensionador automático de cluster](/docs/containers?topic=containers-ca#ca), para estender sua infraestrutura de cluster.</li>
     </ul>
     <br><br>
     **As suas responsabilidades**:
     <ul>
     <li>Use as ferramentas de API, CLI ou console para [aplicar](/docs/containers?topic=containers-update#update) as atualizações principais e secundárias fornecidas do principal do Kubernetes e as atualizações principais, secundárias e de correção do nó do trabalhador.</li>
     <li>Use as ferramentas de API, CLI ou console para [recuperar](/docs/containers?topic=containers-cs_troubleshoot#cs_troubleshoot) seus recursos de infraestrutura ou configure a [Recuperação automática do nó do trabalhador](/docs/containers?topic=containers-health#autorecovery) opcional.</li></ul>
     <br><br></td>
      </tr>
    <tr>
      <td align="center"><img src="images/icon_locked.svg" alt="Ícone de bloqueio"/><br>Ambiente altamente seguro</td>
      <td>
      **Responsabilidades da IBM**:
      <ul>
      <li>Mantenha controles proporcionais a [diversos padrões de conformidade do mercado](/docs/containers?topic=containers-faqs#standards), como PCI DSS.</li>
      <li>Monitore, isole e recupere o cluster do principal.</li>
      <li>Forneça réplicas altamente disponíveis dos componentes do servidor de API, do etcd, do planejador e do gerenciador do controlador do principal do Kubernetes para proteger-se contra uma indisponibilidade principal.</li>
      <li>Aplique automaticamente atualizações principais de correção de segurança e forneça atualizações de correção de segurança do nó do trabalhador.</li>
      <li>Ative determinadas configurações de segurança, como discos criptografados em nós do trabalhador</li>
      <li>Desative determinadas ações inseguras para nós do trabalhador, como não permitir o SSH de usuários no host.</li>
      <li>Criptografe a comunicação entre os nós principal e do trabalhador com TLS.</li>
      <li>Forneça imagens Linux compatíveis com o CIS para os sistemas operacionais do nó do trabalhador.</li>
      <li>Monitore continuamente as imagens do nó principal e do trabalhador para detectar problemas de conformidade de vulnerabilidade e segurança.</li>
      <li>Provisione nós do trabalhador com duas partições de dados SSD locais criptografadas de AES de 256 bits.</li>
      <li>Provisione opções para a conectividade de rede de cluster, como terminais em serviço público e privado.</li>
      <li>Provisione opções de isolamento de cálculo, como máquinas virtuais dedicadas ou bare metal.</li>
      <li>Integre o controle de acesso baseado em função (RBAC) do Kubernetes com o {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM).</li>
      </ul>
      <br><br>
      **As suas responsabilidades**:
      <ul>
      <li>Use as ferramentas de API, CLI ou console para aplicar as [atualizações de correção de segurança](/docs/containers?topic=containers-changelog#changelog) fornecidas para os nós do trabalhador.</li>
      <li>Escolha como configurar sua [rede de cluster](/docs/containers?topic=containers-plan_clusters) e defina outras [configurações de segurança](/docs/containers?topic=containers-security#security) para atender às necessidades de segurança e conformidade de sua carga de trabalho. Se aplicável, configure seu [firewall](/docs/containers?topic=containers-firewall#firewall).</li></ul>
      <br><br></td>
      </tr>

      <tr>
        <td align="center"><img src="images/icon_code.svg" alt="Ícone de colchetes de código"/><br>Orquestração de aplicativo</td>
        <td>
        **Responsabilidades da IBM**:
        <ul>
        <li>Provisione clusters com componentes do Kubernetes instalados para que seja possível acessar a API do Kubernetes.</li>
        <li>Forneça um número de complementos gerenciados para estender os recursos de seu aplicativo, como o [Istio](/docs/containers?topic=containers-istio#istio) e o [Knative](/docs/containers?topic=containers-serverless-apps-knative). A manutenção é simplificada para você porque a IBM fornece a instalação e as atualizações para os complementos gerenciados.</li>
        <li>Provisione integração de cluster com tecnologias de parceria de terceiro selecionadas, como o {{site.data.keyword.la_short}}, o {{site.data.keyword.mon_short}} e o Portworx.</li>
        <li>Forneça a automação para ativar a ligação de serviços para outros serviços do {{site.data.keyword.cloud_notm}}.</li>
        <li>Crie clusters com segredos de pull de imagem para que suas implementações no namespace `default` do Kubernetes possam fazer pull de imagens do {{site.data.keyword.registrylong_notm}}.</li>
        <li>Forneça classes de armazenamento e plug-ins para suportar volumes persistentes para uso com seus aplicativos.</li>
        <li>Crie clusters com endereços IP de sub-rede reservados para o uso de exposição externa de aplicativos.</li>
        <li>Suporte balanceadores de carga públicos e privados nativos do Kubernetes e rotas do Ingress para expor serviços externamente.</li>
        </ul>
        <br><br>
        **As suas responsabilidades**:
        <ul>
        <li>Use as ferramentas e os recursos fornecidos para [configurar e implementar](/docs/containers?topic=containers-app#app), [configurar permissões](/docs/containers?topic=containers-users#users), [integrar outros serviços](/docs/containers?topic=containers-supported_integrations#supported_integrations), [entregar externamente](/docs/containers?topic=containers-cs_network_planning#cs_network_planning), [monitorar o funcionamento](/docs/containers?topic=containers-health#health), [salvar, fazer backup e restaurar dados](/docs/containers?topic=containers-storage_planning#storage_planning), caso contrário, gerencie suas cargas de trabalho [altamente disponíveis](/docs/containers?topic=containers-ha#ha) e resilientes.</li>
        </ul>
        </td>
        </tr>
  </tbody>
  </table>

<br />


## Abuso do Red Hat OpenShift on IBM Cloud
{: #terms}

Os clientes não podem usar o Red Hat OpenShift on IBM Cloud incorretamente.
{:shortdesc}

Uso inadequado inclui:

*   Qualquer atividade ilegal
*   Distribuição ou execução de malware
*   Danificar o Red Hat OpenShift on IBM Cloud ou interferir com o uso do Red Hat OpenShift on IBM Cloud por alguma pessoa
*   Prejudicar ou interferir no uso de alguém de qualquer outro serviço ou sistema
*   Acesso não autorizado a qualquer serviço ou sistema
*   Modificação não autorizada de qualquer serviço ou sistema
*   Violação dos direitos de outros

Veja [Termos dos serviços
de nuvem](/docs/overview/terms-of-use?topic=overview-terms#terms) para obter os termos gerais de uso.


