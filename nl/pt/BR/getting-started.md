---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, containers, clusters, roks, rhoks, rhos

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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Introdução ao Red Hat OpenShift on IBM Cloud
{: #getting-started}

Com o Red Hat OpenShift on IBM Cloud, é possível criar clusters do {{site.data.keyword.containerlong_notm}} com nós do trabalhador que vêm instalados com o software de orquestração Red Hat OpenShift on IBM Cloud Container Platform. Você obtém todas as [vantagens do {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-responsibilities_iks) gerenciado para seu ambiente de infraestrutura de cluster ao usar o [conjunto de ferramentas e o catálogo do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/welcome/index.html) que são executados no Red Hat Enterprise Linux para suas implementações de app.
{: shortdesc}

Para concluir o tutorial de introdução, use uma conta Pré-paga do {{site.data.keyword.cloud_notm}} cujo proprietário seja você ou na qual você tenha privilégios de administrador integrais. Este tutorial de introdução foca em configurar um cluster e um app de amostra rapidamente usando o console do {{site.data.keyword.cloud_notm}}. Para obter mais informações sobe como usar a CLI para criar seu cluster do OpenShift e implementar um app, confira este [tutorial](/docs/openshift?topic=openshift-openshift_tutorial).

## Criando um cluster do OpenShift
{: #openshift_gs_cluster}

Crie um cluster do Red Hat OpenShift on IBM Cloud no console do {{site.data.keyword.containerlong_notm}}. Os clusters do OpenShift executam a versão 3.11, que inclui o Kubernetes versão 1.11. O sistema operacional é o Red Hat Enterprise Linux 7.
{: shortdesc}

Deseja aprender mais sobre a customização da configuração do seu cluster com a CLI? Confira [Criando um cluster do OpenShift](/docs/openshift?topic=openshift-openshift-create-cluster).
{: tip}

1.  Efetue login em sua [conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/).
2.  No **Catálogo**, clique em [**Cluster do Red Hat OpenShift** ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")]](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster) e, em seguida, clique em **Criar**.
3.  Escolha os detalhes e o nome da configuração do cluster.
    *   Insira um nome para seu cluster e selecione o grupo de recursos que deseja designar ao seu cluster.
    *   Insira tags que deseja incluir em seu cluster. As tags podem ajudar a organizar e localizar seus clusters mais facilmente em sua conta do {{site.data.keyword.cloud_notm}}.
    *   Para a **Localização**, configure a **Geografia** e, em seguida, selecione qualquer uma das seis [Localizações](/docs/openshift?topic=openshift-regions-and-zones) **metropolitanas** de várias zonas mundiais para usar para suas **Zonas do trabalhador**.
    *   Para o **Conjunto de trabalhadores padrão**, escolha um tipo disponível para seus nós do trabalhador. O Red Hat OpenShift on IBM Cloud suporta o OpenShift versão 3.11 somente, o que inclui o Kubernetes versão 1.11. O sistema operacional é o Red Hat Enterprise Linux 7.

    *   Configure um número de nós do trabalhador a serem criados por zona, como `3`.
4.  Para concluir, clique em **Criar cluster**.<p class="note">A criação do cluster pode levar algum tempo para ser concluída. Após o estado do cluster mostrar **Normal**, a rede de cluster e o componente de balanceamento de carga levarão cerca de mais 10 minutos para implementar e atualizar o domínio do cluster que você usa para o console da web do OpenShift e outras rotas. </p>
5.  Verifique se a configuração do seu cluster foi concluída antes de continuar para a próxima etapa, conferindo se o **Subdomínio do Ingress** na página de detalhes do cluster segue um padrão de `<cluster_name>.<region>.containers.appdomain.cloud`.

<br />


## Implementando um app com o catálogo do OpenShift
{: #openshift_gs_app}

No console do OpenShift, é possível implementar um dos apps de catálogo integrados.
{: shortdesc}

1.  Na página de detalhes do cluster, clique em **Console da web do OpenShift**.
2.  Na área de janela **Introdução**, clique em **Criar projeto**. Insira um nome para seu nome do projeto e clique em **Criar**. Se você já tiver projetos existentes, o nome da sua área de janela mudará para **Meus projetos**.
3.  Clique no nome do seu projeto e, em seguida, clique em **Procurar no catálogo**.
4.  Clique em um app a ser implementado. Por exemplo, na guia **Idioma**, selecione **JavaScript** e, em seguida, clique em **Node.js**. O assistente Node.js é aberto.
    1.  Na guia *Informações*, clique em **Avançar**.
    2.  Na guia *Configuração*, clique em **Tentar repositório de amostra**.
    3.  Na guia *Resultados*, o app `nodejs-ex` é criado. Clique em **Fechar**.
5.  Aguarde alguns minutos para que os pods sejam implementados. Para verificar o status dos pods, clique em **Aplicativos > Pods**. Deve-se ver um pod `nodejs-ex-build` em um estado **Concluído** e um pod `nodejs-ex` em um estado **Em execução**.
6.  Quando ambos os pods estiverem disponíveis, clique em **Aplicativos > Rotas**.
7.  Clique no **Nome do host** do seu app `nodejs-ex`. Uma nova guia no seu navegador se abrirá com uma mensagem semelhante à mostrada a seguir.
    ```
    Bem-vindo ao seu aplicativo Node.js no OpenShift
    ```
    {: screen}
8.  **Opcional**: para limpar os recursos que você criou, clique no nome do projeto na barra de menus e, em seguida, em **Visualizar todos os projetos**. Clique no ícone **Mais opções > Excluir projeto**.

<br />


## O que Vem a Seguir?
{: #openshift_gs_next}

Conclua o [tutorial do Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-openshift_tutorial) para:
* Configurar sua CLI do {{site.data.keyword.cloud_notm}} e do OpenShift.
* Implementar um app que usa um serviço do {{site.data.keyword.cloud_notm}}.

<br>
Para obter mais informações sobre como trabalhar com seus apps e serviços de roteamento, consulte o [Guia do desenvolvedor do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")]](https://docs.openshift.com/container-platform/3.11/dev_guide/index.html).

<br />

