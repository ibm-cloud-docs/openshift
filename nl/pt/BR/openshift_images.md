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

# Construindo imagens para seus apps 
{: #openshift-images}

Os clusters do {{site.data.keyword.openshiftlong}} incluem um registro interno para construir, implementar e gerenciar imagens de contêiner localmente. Para que um registro privado gerencie e controle o acesso a imagens em sua empresa, também é possível configurar seu cluster para que use o {{site.data.keyword.registrylong}}.
{: shortdesc}

## Usando o registro interno
{: #openshift_internal_registry}

Os clusters do OpenShift são configurados por padrão com um registro interno. Para obter mais informações, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html#install-config-registry-overview).
{: shortdesc}

## Usando o {{site.data.keyword.registrylong_notm}}
{: #openshift_iccr}

Se você desejar usar imagens que estão armazenadas em seus nomes de domínio `icr.io` do {{site.data.keyword.registrylong_notm}} privado remoto, deverá criar segredos de pull de imagem para cada registro global e regional. Em seguida, inclua os segredos de pull da imagem em cada projeto e em uma conta de serviço para cada projeto ou para cada implementação.
{: shortdesc}

Para obter mais informações, consulte os tópicos a seguir nos docs do {{site.data.keyword.containershort_notm}}.
* [Entendendo como autorizar seu cluster para fazer pull de imagens por meio de um registro](/docs/containers?topic=containers-images#cluster_registry_auth).
* [Copiando os segredos `default-<region>-icr-io` ](/docs/containers?topic=containers-images#copy_imagePullSecret) do namespace `default` para o namespace do qual você deseja fazer pull de imagens.
* [Criando seu próprio segredo de pull de imagem](/docs/containers?topic=containers-images#other_registry_accounts).
* [Incluindo o segredo de pull de imagem](/docs/containers?topic=containers-images#use_imagePullSecret) em sua configuração de implementação ou na conta de serviço do namespace.
