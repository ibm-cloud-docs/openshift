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
{:download: .download}
{:preview: .preview}

# Aprimorando recursos de cluster com integrações
{: #openshift_integrations}

Com o {{site.data.keyword.openshiftlong}}, você tem muitas formas de aprimorar os recursos do cluster e do app com o conteúdo IBM e de terceiros, como IA, segurança, bancos de dados, criação de log, monitoramento e mais. Aprenda sobre quais integrações estão disponíveis e como integrar esses serviços com seu cluster.
{: shortdesc}

## Integrações disponíveis
{: #openshift_available_integrations}

Saiba mais sobre as integrações do {{site.data.keyword.cloud_notm}} e de terceiros a seguir para clusters do OpenShift.
{: shortdesc}

<dl>
  <dt>Serviços de plataforma do {{site.data.keyword.cloud_notm}}</dt>
  <dd>Os serviços da plataforma do {{site.data.keyword.cloud_notm}} que suportam chaves de serviço podem ser integrados usando a [ligação de serviços](#oc_service_binding). Para localizar uma visão geral dos serviços populares do {{site.data.keyword.cloud_notm}}, consulte [Integrações populares](/docs/containers?topic=containers-supported_integrations#popular_services).</dd>

  <dt>Serviços de infraestrutura clássica do {{site.data.keyword.cloud_notm}}</dt>
  <dd>Seu cluster do OpenShift é baseado em serviços de infraestrutura clássica do {{site.data.keyword.cloud_notm}} totalmente integrados, como Virtual Servers, Bare Metal Servers ou VLANs. Você cria e trabalha com essas instâncias de serviços usando a API, a CLI ou o console do {{site.data.keyword.containerlong_notm}}.<br><br>
  Para proteger sua rede de cluster ou se conectar a um data center no local, é possível configurar uma das opções a seguir:
    <ul><li>[Serviço VPN IPSec do strongSwan](/docs/containers?topic=containers-vpn#vpn-setup)</li>
    <li>[{{site.data.keyword.BluDirectLink}}](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link)</li>
    <li>[Virtual Router Appliance (VRA)](/docs/containers?topic=containers-vpn#vyatta)</li>
    <li>[Fortigate Security Appliance (FSA)](/docs/services/vmwaresolutions/services?topic=vmware-solutions-fsa_considerations)</li></ul></dd>

  <dt>Armazenamento do {{site.data.keyword.cloud_notm}}</dt>
  <dd>As soluções de armazenamento persistente suportadas, como {{site.data.keyword.cloud_notm}} File Storage, {{site.data.keyword.cloud_notm}} Block Storage ou {{site.data.keyword.cos_full_notm}} são integradas como drivers flex do Kubernetes e podem ser configuradas usando [gráficos do Helm](#oc_helm). A documentação de armazenamento para cada solução inclui instruções para instalar e gerenciar o armazenamento. Para obter mais informações sobre a escolha de uma solução de armazenamento persistente, consulte [Planejando armazenamento persistente altamente disponível](/docs/openshift?topic=containers-storage_planning).</dd>

  <dt>Ajustador automático de escala de cluster</dt>
  <dd>Com o plug-in `ibm-iks-cluster-autoscaler`, é possível escalar os conjuntos do trabalhador em seu cluster automaticamente para aumentar ou diminuir o número de nós do trabalhador no conjunto do trabalhador baseado nas solicitações de dimensionamento de suas cargas de trabalho planejadas. Para obter mais informações, consulte [Escalando clusters](/docs/containers?topic=containers-ca) nos docs do {{site.data.keyword.containerlong_notm}}.</dd>

  <dt>Istio para rede de serviço</dt>
  <dd>Ao contrário de clusters Kubernetes da comunidade, o <a href="https://www.ibm.com/cloud/info/istio" target="_blank">Istio <img src="../icons/launch-glyph.svg" alt="Ícone de link externo"></a> não está disponível como um complemento gerenciado para clusters do OpenShift. Em vez disso, use o projeto de Rede de serviço do Red Hat OpenShift. Para obter mais informações, consulte [os docs de instalação do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/servicemesh-install/servicemesh-install.html).</dd>

  <dt>Knative para apps sem servidor</dt>
  <dd>Ao contrário de clusters Kubernetes da comunidade, o <a href="https://github.com/knative/docs" target="_blank">Knative <img src="../icons/launch-glyph.svg" alt="Ícone de link externo"></a> não está disponível como um complemento gerenciado para clusters do OpenShift. Em vez disso, teste o Knative na visualização do desenvolvedor do OpenShift. Para obter mais informações, consulte [os docs de instalação do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/openshift-knative/docs).</dd>

  <dt>Kubernetes Terminal</dt>
  <dd>O [complemento Kubernetes Terminal](/docs/containers?topic=containers-cs_cli_install#cli_web) está disponível somente para o cluster Kubernetes da comunidade, não para clusters do OpenShift.</dd>

  <dt>{{site.data.keyword.la_full_notm}}</dt>
  <dd>Inclua recursos de gerenciamento de log no cluster implementando LogDNA como um serviço de terceiro para seus nós do trabalhador para gerenciar logs dos contêineres de pod. Para obter mais informações, consulte os docs a seguir.<ul>
    <li>[Sobre a parceria LogDNA](/docs/containers?topic=containers-service-partners#logdna-partner).</li>
    <li>[Configurando o LogDNA em um cluster do OpenShift](/docs/openshift?topic=openshift-openshift_health#openshift_logdna).</li>
    <li>[Tutorial: gerenciando logs do cluster Kubernetes com o {{site.data.keyword.loganalysisfull_notm}} com LogDNA](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-kube#kube).</li></ul></dd>

  <dt>Razee</dt>
  <dd>O [Razee ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://razee.io/) é um projeto de software livre que automatiza e gerencia a implementação de recursos do Kubernetes em clusters, ambientes e provedores em nuvem, além de ajudar a visualizar informações de implementação para seus recursos para que seja possível monitorar o processo de lançamento e localizar problemas de implementação mais rapidamente. Para obter mais informações sobre o Razee e como configurá-lo em seu cluster para automatizar seu processo de implementação, consulte a [documentação do Razee ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/razee-io/Razee).</dd>

  <dt>{{site.data.keyword.mon_full_notm}}</dt>
  <dd>Obtenha visibilidade operacional para o desempenho e o funcionamento de seus apps implementando o Sysdig como um serviço de terceiro para os nós do trabalhador para encaminhar métricas para o {{site.data.keyword.monitoringlong}}. Para obter mais informações, consulte os docs a seguir.<ul>
    <li>[Sobre a parceria Sysdig](/docs/containers?topic=containers-service-partners#sydig-partner).</li>
    <li>[Configurando o Sysdig em um cluster do OpenShift](/docs/openshift?topic=openshift-openshift_health#openshift_sysdig).</li>
    <li>[Tutorial: analisando métricas para um app que é implementado em um cluster Kubernetes](/docs/services/Monitoring-with-Sysdig/tutorials?topic=Sysdig-kubernetes_cluster#kubernetes_cluster).</li></ul></dd>

  <dt>Outras integrações de terceiros</dt>
  <dd>É possível instalar muitas outras integrações em seu cluster do OpenShift, como por meio do catálogo do OpenShift, Operadores, gráficos do Helm ou instalações de software livre do tipo faça-você-mesmo. Assegure-se de que esses apps sejam compatíveis com seu cluster do OpenShift e versão do Kubernetes. Por exemplo, pode ser necessário [atualizar o app](/docs/openshift?topic=openshift-openshift_apps) para que a instalação seja bem-sucedida.</dd>

</dl>

<br />


## Incluindo integrações em seu cluster do OpenShift
{: #openshift_adding_services}

É possível incluir serviços em seu cluster do Red Hat OpenShift on IBM Cloud de várias formas, incluindo ligação de serviços, gráficos do Helm e operadores. Se desejar instalar apps de software livre, assegure-se de que esses apps sejam compatíveis com seu cluster do OpenShift e versão do Kubernetes. Por exemplo, pode ser necessário [atualizar o app](/docs/openshift?topic=openshift-openshift_apps) para que a instalação seja bem-sucedida.
{: shortdesc}

### IBM Cloud Paks
{: #oc_cloud_paks}

Os [IBM Cloud Paks&trade; ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/paks/) são componentes de middleware IBM e de software livre conteinerizados que você está licenciado para usar no [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/) como parte de sua solução de nuvem híbrida. Os IBM Cloud Paks são executados exclusivamente em clusters do OpenShift, não em clusters Kubernetes da comunidade. Para usar o IBM Cloud Paks, deve-se configurar seu ambiente em cluster como a seguir.
{: shortdesc}

1. No projeto que você deseja implementar o Cloud Pak, assegure-se de [configurar o segredo de pull de imagem para acessar imagens armazenadas no {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-openshift-images#openshift_iccr).
2. Importe o Cloud Pak do Passport Advantage para seu registro. Os métodos variam dependendo do Cloud Pak.
   * Para ambientes de nuvem pública, é possível usar a ferramenta da CLI [`ibmcloud cr ppa-archive-load`](/docs/services/Registry?topic=registry-ts_index#ts_ppa_import).
   * Se você tiver o ICP Common Services instalado em seu cluster, será possível usar a ferramenta da CLI [`cloudctl catalog load-archive`](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/app_center/add_package_offline.html).
   * Alguns Cloud Paks, como {{site.data.keyword.icp4dfull_notm}}, enviam por push a imagem do registro para você como parte de seu processo de instalação.
3. Siga as instruções que são específicas a cada instalação do Cloud Pak, como configurar os valores de gráfico do Helm para trabalhar em restrições de contexto de segurança do OpenShift.

### Ligação de serviços do {{site.data.keyword.cloud_notm}}
{: #oc_service_binding}

Para acessar os serviços do {{site.data.keyword.cloud_notm}} em sua conta, é possível criar credenciais de serviço e armazenar essas credenciais em um segredo do Kubernetes em seu cluster. Para obter mais informações, consulte [Incluindo serviços usando a ligação de serviços do {{site.data.keyword.cloud_notm}}](/docs/containers?topic=containers-service-binding).

### Gráficos do Helm
{: #oc_helm}

[O Helm ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://helm.sh) é um gerenciador de pacotes do Kubernetes que usa gráficos do Helm para definir, instalar e fazer upgrade de aplicativos complexos do Kubernetes em seu cluster. Os gráficos do Helm empacotam as especificações para gerar arquivos YAML para recursos do Kubernetes que constroem seu aplicativo. Como o OpenShift configura restrições de contexto de segurança mais estritas para o Kubernetes da comunidade, pode ser necessário modificar sua implementação do Helm antes de instalar o gráfico. Para instalar o Helm, consulte os [docs do {{site.data.keyword.containershort_notm}}](/docs/containers?topic=containers-helm).
{: shortdesc}

### Operadores
{: #oc_operators}

Em vez do Helm, é possível usar [Operadores ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/4.1/applications/operators/olm-what-operators-are.html) para empacotar, implementar e atualizar seus apps. Os operadores estão disponíveis somente para versões 4.1 do OpenShift. Enquanto isso, é possível testar o [Operador experimental do {{site.data.keyword.cloud_notm}}![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.ibm.com/seed/olm/blob/master/pocs/openshift-ibmcloud/README.md).
{: shortdesc}
