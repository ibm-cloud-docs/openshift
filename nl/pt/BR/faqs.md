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
{:faq: data-hd-content-type='faq'}


# Perguntas frequentes
{: #faqs}

Revise as perguntas mais frequentes sobre o uso do {{site.data.keyword.openshiftlong}}.
{: shortdesc}

## Quais plataformas de contêiner estão disponíveis para meu cluster?
{: #container_platforms}
{: faq}

Com o {{site.data.keyword.containerlong_notm}}, é possível selecionar entre duas plataformas de gerenciamento de contêiner: a versão da IBM do Kubernetes da comunidade e o Red Hat OpenShift on IBM Cloud. A plataforma de contêiner que você seleciona é instalada no cluster mestre e nos nós do trabalhador. Posteriormente, é possível [atualizar a versão](/docs/containers?topic=containers-update#update), mas não é possível retroceder para uma versão anterior ou alternar para uma plataforma de contêiner diferente. Se você desejar usar múltiplas plataformas de contêiner, crie um cluster separado para cada uma delas.

Para obter mais informações, consulte [Comparação entre clusters OpenShift e Kubernetes da comunidade](/docs/openshift?topic=openshift-why_openshift#openshift_kubernetes).

<dl>
  <dt>Kubernetes</dt>
    <dd>[Kubernetes ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/) é uma plataforma de orquestração de contêiner de software livre de nível de produção que pode ser usada para automatizar, escalar e gerenciar seus aplicativos conteinerizados executados em um sistema operacional Ubuntu. Com a [versão do {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-cs_versions#cs_versions), você tem acesso aos recursos da API do Kubernetes da comunidade que são considerados **beta** ou mais recentes pela comunidade. Os recursos **alpha** do Kubernetes, que estão sujeitos a mudança, geralmente não são ativados por padrão. Com Kubernetes, é possível combinar vários recursos, como segredos, implementações e serviços para criar e gerenciar com segurança os aplicativos altamente disponíveis e conteinerizados.<br><br>
    Para iniciar, [crie um cluster Kubernetes](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial).</dd>
  <dt>OpenShift</dt>
    <dd>O Red Hat OpenShift on IBM Cloud é uma plataforma baseada em Kubernetes projetada especialmente para acelerar os processos de entrega de aplicativos conteinerizados que são executados em um sistema operacional Red Hat Enterprise Linux 7. É possível orquestrar e escalar suas cargas de trabalho do OpenShift existentes por nuvens no local e fora do local para uma solução híbrida móvel que funciona da mesma forma em cenários com múltiplas nuvens. <br><br>
    Para iniciar, tente o [Tutorial do Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-openshift_tutorial).</dd>
</dl>

## Posso criar um cluster do OpenShift grátis?
{: #openshift_free}
{: faq}

É possível criar apenas clusters padrão do OpenShift. Se desejar testar os recursos do Kubernetes, [crie um cluster Kubernetes grátis](/docs/containers?topic=containers-clusters#clusters_free) e [implemente alguns apps](/docs/containers?topic=containers-app). Em seguida, implemente novamente os apps testados no cluster Kubernetes para o [cluster do OpenShift](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app).

## Posso converter meu cluster beta do OpenShift para um cluster em GA?
{: #openshift_beta_convert}
{: faq}

É possível criar um cluster em GA e, em seguida, implementar novamente quaisquer apps que você usar nos clusters beta antes que estes sejam removidos. Os clusters beta serão removidos até 31 de agosto de 2019 à 0h UTC (30 dias após o Red Hat OpenShift on IBM Cloud ser fornecido em disponibilidade geral). Para ver um exemplo da obtenção de todos os arquivos de configuração de um projeto, consulte os [docs do OpenShift](https://docs.openshift.com/dedicated/admin_guide/assembly_backing-up-restoring-project-application.html).

## O serviço do OpenShift suporta quais versões do Kubernetes?
{: #supported_kube_versions}
{: faq}

A versão do OpenShift suportada é a 3.11, que inclui o Kubernetes 1.11.

## Pelo que sou cobrado quando uso um OpenShift?
{: #openshift_charges}
{: faq}

Para clusters do Red Hat OpenShift on IBM Cloud, você é cobrado pelos mesmos componentes que nos clusters do {{site.data.keyword.containerlong_notm}}. Para obter mais informações, consulte [Pelo que sou cobrado quando uso o {{site.data.keyword.containerlong_notm}}?](/docs/containers?topic=containers-faqs#charges)

Além disso, seus nós do trabalhador são instalados com o sistema operacional Red Hat Enterprise Linux, o que aumenta o preço das máquinas do nó do trabalhador. Deve-se também deve ter uma licença do OpenShift, que incorre em custos mensais além dos custos de VM por hora ou custos de bare metal mensais. A licença do OpenShift é para cada dois núcleos do tipo de nó do trabalhador. Se você excluir seu nó do trabalhador antes do término do mês, sua licença mensal estará disponível para outros nós do trabalhador no conjunto de trabalhadores a ser usado.
