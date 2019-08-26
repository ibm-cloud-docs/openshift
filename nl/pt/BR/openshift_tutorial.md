---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: kubernetes, iks, oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

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

# Tutorial: criando um cluster do Red Hat OpenShift on IBM Cloud
{: #openshift_tutorial}

Com o Red Hat OpenShift on IBM Cloud, é possível criar clusters do {{site.data.keyword.containerlong_notm}} com nós do trabalhador que vêm instalados com o software de orquestração Red Hat OpenShift on IBM Cloud Container Platform. Você obtém todas as [vantagens do {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-responsibilities_iks) gerenciado para seu ambiente de infraestrutura de cluster ao usar o [conjunto de ferramentas e o catálogo do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/welcome/index.html) que são executados no Red Hat Enterprise Linux para suas implementações de app.
{: shortdesc}

Os nós do trabalhador do OpenShift estão disponíveis para contas pagas e clusters padrão somente. O Red Hat OpenShift on IBM Cloud suporta o OpenShift versão 3.11 somente, o que inclui o Kubernetes versão 1.11. O sistema operacional é o Red Hat Enterprise Linux 7.
{: note}


## Objetivos
{: #openshift_objectives}

Nas lições do tutorial, você cria um cluster padrão do Red Hat OpenShift on IBM Cloud, abre o console do OpenShift, acessa componentes integrados do OpenShift, implementa um app que usa serviços do {{site.data.keyword.cloud_notm}} em um projeto do OpenShift e expõe o app em uma rota do OpenShift para que os usuários externos possam acessar o serviço.
{: shortdesc}

<img src="/images/roks_tutorial.png" width="600" alt="Diagrama do tutorial do OpenShift" style="width:600px; border-style: none"/>

## Tempo
Necessário
{: #openshift_time}
45 minutos

## Público Alvo
{: #openshift_audience}

Este tutorial é para administradores de cluster que desejam aprender como criar um cluster do Red Hat OpenShift on IBM Cloud pela primeira vez.
{: shortdesc}

## Pré-requisitos
{: #openshift_prereqs}

*   Assegure-se de que você tenha as políticas de acesso do {{site.data.keyword.cloud_notm}} IAM a seguir.
    *   A [função da plataforma **Administrador**](/docs/containers?topic=containers-users#platform) para o {{site.data.keyword.containerlong_notm}}
    *   A [função do serviço **Gravador** ou **Gerenciador**](/docs/containers?topic=containers-users#platform) para o {{site.data.keyword.containerlong_notm}}
    *   A [função da plataforma **Administrador**](/docs/containers?topic=containers-users#platform) para o {{site.data.keyword.registrylong_notm}}
*    Certifique-se de que a [chave de API](/docs/containers?topic=containers-users#api_key) para a região e o grupo de recursos do {{site.data.keyword.cloud_notm}} esteja configurada com as permissões corretas de infraestrutura, com **Superusuário** ou com as [funções mínimas](/docs/containers?topic=containers-access_reference#infra) para criar um cluster.

<br />


## Lição 1: criando um cluster do Red Hat OpenShift on IBM Cloud
{: #openshift_create_cluster}

Crie um cluster do Red Hat OpenShift on IBM Cloud no {{site.data.keyword.containerlong_notm}}. Para aprender sobre quais componentes são configurados quando você cria um cluster, consulte a [Arquitetura de serviço](/docs/openshift?topic=openshift-openshift-service-arch). O OpenShift está disponível somente para clusters padrão. É possível aprender mais sobre o preço de clusters padrão nas [perguntas mais frequentes](/docs/openshift?topic=openshift-faqs#charges).
{:shortdesc}

1.  Instale as ferramentas de linha de comandos.
    *   [Instale a CLI do {{site.data.keyword.cloud_notm}} (`ibmcloud`), o plug-in do {{site.data.keyword.containershort_notm}} (`ibmcloud oc`) e o plug-in do {{site.data.keyword.registryshort_notm}} (`ibmcloud cr`)](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps).
    *   [Instale as CLIs do OpenShift Origin (`oc`) e do Kubernetes (`kubectl`)](/docs/containers?topic=containers-cs_cli_install#cli_oc).
2.  Efetue login na conta que você configurou para criar clusters do OpenShift. Tenha como destino a região **us-east** ou **eu-gb** e o grupo de recursos. Se você tiver uma conta federada, inclua a sinalização `--sso`.
    ```
    ibmcloud login -r (us-east|eu-gb) [-g default] [--sso]
    ```
    {: pre}
3.  Crie um cluster. O comando a seguir cria um cluster com três nós do trabalhador que têm quatro núcleos e 16 GB de memória em Washington, DC. Se você tiver VLANs existentes que queira usar, obtenha os IDs de VLAN executando `ibmcloud oc vlans --zone <zone>`.
    ```
    ibmcloud oc cluster-create --name my_openshift --location wdc04 --kube-version 3.11_openshift --machine-type b3c.4x16.encrypted  --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}
4.  Liste os detalhes do cluster. Revise o **Estado** do cluster, verifique o **Subdomínio do Ingress** e anote a **URL principal**.<p class="note">A criação do cluster pode levar algum tempo para ser concluída. Depois que o estado do cluster mostra **Normal**, a rede de cluster e os componentes de balanceamento de carga levam mais de 10 minutos para implementar e atualizar o domínio do cluster usado para o console da web do OpenShift e outras rotas. Aguarde até que o cluster esteja pronto antes de continuar com a próxima etapa, verificando se o **Subdomínio do Ingress** segue um padrão de `<cluster_name>.<region>.containers.appdomain.cloud`.</p>
    ```
    ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
    ```
    {: pre}
5.  Faça download dos arquivos de configuração para se conectar ao seu cluster.
    ```
    ibmcloud oc cluster-config --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Quando o download dos arquivos de configuração é concluído, é exibido um comando que pode ser copiado e colado para configurar o caminho para o arquivo de configuração do Kubernetes local como uma variável de ambiente.

    Exemplo para OS X:

    ```
    export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>/kube-config-<datacenter>-<cluster_name>.yml
    ```
    {: screen}
6.  Em seu navegador, navegue para o endereço de sua **URL principal** e anexe `/console`. Por exemplo, `https://c0.containers.cloud.ibm.com:23652/console`.
7.  Na barra de menus do console da web do OpenShift, clique em seu perfil **IAM#user.name@email.com > Copiar comando de login**. Cole o comando de login `oc` copiado em seu terminal para autenticar por meio da CLI.<p class="tip">Salve a URL do cluster principal para acessar o console do OpenShift posteriormente. Em sessões futuras, será possível ignorar a etapa `cluster-config` e copiar o comando de login por meio do console.</p>
8.  Verifique se os comandos `oc` são executados corretamente com seu cluster verificando a versão.

    ```
    oc version
    ```
    {: pre}

    Saída de exemplo:

    ```
    oc v3.11.0+0cbc58b
    kubernetes v1.11.0+d4cacc0
    features: Basic-Auth

    Server https://c0.containers.cloud.ibm.com:23652
    openshift v3.11.98
    kubernetes v1.11.0+d4cacc0
    ```
    {: screen}

    Se não for possível executar operações que requeiram permissões de Administrador, como listar todos os nós do trabalhador ou pods em um cluster, faça download dos certificados TLS e arquivos de permissão para o administrador do cluster executando o comando `ibmcloud oc cluster-config --cluster <cluster_name_or_ID> --admin`.
    {: tip}

<br />


## Lição 2: navegando no console do OpenShift
{: #openshift_oc_console}

O Red Hat OpenShift on IBM Cloud é fornecido com serviços integrados que podem ser usados para ajudar a operar seu cluster, como o console do OpenShift.
{:shortdesc}

1.  No console dos [clusters do {{site.data.keyword.containerlong_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift), selecione seu cluster do OpenShift e, em seguida, clique em **Console da web do OpenShift**.
2.  Explore as diferentes áreas do console do OpenShift, clicando no menu suspenso na barra de menus **OpenShift Container Platform**.
    * **Catálogo de serviços**: navegue pelo catálogo de serviços integrados que podem ser implementados no OpenShift. Por exemplo, se você já tiver um app `node.js` hospedado no GitHub, será possível clicar na guia **Idiomas** e implementar um app **JavaScript**. A área de janela **Meus projetos** fornece uma visão rápida de todos os projetos aos quais você tem acesso, e clicar em um projeto leva você até o Console do aplicativo.
    * **Console do aplicativo**: para cada namespace do projeto ao qual você tem acesso, é possível gerenciar e visualizar logs para seus recursos do OpenShift, como pods, serviços, rotas, construções, imagens ou solicitações de volume persistente. Também é possível incluir serviços do catálogo no projeto.
    * **Console do cluster**: para administradores em todo o cluster em todos os projetos no cluster, é possível gerenciar projetos, contas de serviço, funções RBAC, ligações de função e cotas de recursos. Também é possível ver visualizações combinadas do status e de eventos dos recursos dentro do cluster.
3.  Para continuar trabalhando com seu cluster no terminal: no Console de serviço ou no Console do aplicativo, clique em seu perfil **IAM#user.name@email.com > Copiar comando de login**. Cole o comando de login `oc` copiado em seu terminal para autenticar por meio da CLI.

<br />


## Lição 3: implementando um app em seu cluster do OpenShift
{: #openshift_deploy_app}

Com o Red Hat OpenShift on IBM Cloud, é possível criar um novo app e expor seu serviço de app por meio de um roteador do OpenShift para usuários externos usarem.
{: shortdesc}

Se você fez uma pausa na última lição e iniciou um novo terminal, certifique-se de efetuar login novamente em seu cluster. Abra seu console da web do OpenShift em `https://<master_URL>/console`. Por exemplo, `https://c0.containers.cloud.ibm.com:23652/console`. Em seguida, na barra de menus, clique em seu perfil **IAM#user.name@email.com > Copiar comando de login** e cole o comando de login copiado `oc` em seu terminal para autenticar por meio da CLI.
{: tip}

1.  Crie um projeto para seu app Hello World. Um projeto é uma versão do OpenShift de um namespace do Kubernetes com anotações adicionais.
    ```
    oc new-project hello-world
    ```
    {: pre}
2.  Construa o aplicativo de amostra [por meio do código-fonte ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM/container-service-getting-started-wt). Com o comando `new-app` do OpenShift, é possível referir-se a um diretório em um repositório remoto que contenha o Dockerfile e o código do app para construir sua imagem. O comando constrói a imagem, armazena a imagem no registro do Docker local e cria as configurações de implementação de app (`dc`) e os serviços (`svc`). Para obter mais informações sobre a criação de novos apps, [consulte os docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/dev_guide/application_lifecycle/new_app.html).
    ```
    oc new-app --name hello-world https://github.com/IBM/container-service-getting-started-wt --context-dir="Lab 1"
    ```
    {: pre}
3.  Verifique se os componentes do app Hello World de amostra são criados.
    1.  Liste os serviços **hello-world** e anote o nome do serviço. Seu app atende o tráfego nesses endereços IP do cluster interno, a menos que você crie uma rota para o serviço para que o roteador possa encaminhar solicitações de tráfego externo para o app.
        ```
        oc get svc -n hello-world
        ```
        {: pre}

        Saída de exemplo:
        ```
        NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
        hello-world   ClusterIP   172.21.xxx.xxx   <nones>       8080/TCP   31m
        ```
        {: screen}
    2.  Liste os pods. Os pods com `build` no nome são tarefas **Concluídas** como parte do novo processo de construção do app. Certifique-se de que o status do pod **hello-world** seja **Em execução**.
        ```
        oc get pods -n hello-world
        ```
        {: pre}

        Saída de exemplo:
        ```
        NAME                READY     STATUS             RESTARTS   AGE
        hello-world-9cv7d   1/1       Running            0          30m
        hello-world-build   0/1       Completed          0          31m
        ```
        {: screen}
4.  Configure uma rota para que seja possível acessar publicamente o serviço Hello World. Por padrão, o nome do host está no formato de `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. Se você desejar customizar o nome do host, inclua a sinalização `--hostname=<hostname>`.
    1.  Crie uma rota para o serviço **hello-world**.
        ```
        oc create route edge --service=hello-world -n hello-world
        ```
        {: pre}
    2.  Obtenha o endereço do nome do host da rota por meio da saída de **Host/Porta**.
        ```
        oc get route -n hello-world
        ```
        {: pre}
        Saída de exemplo:
        ```
        NAME          HOST/PORT                         PATH                                        SERVICES      PORT       TERMINATION   WILDCARD
        hello-world   hello-world-hello.world.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud    hello-world   8080-tcp   edge/Allow    None
        ```
        {: screen}
5.  Acesse seu app. Assegure-se de anexar `https://` ao seu nome do host da rota.
    ```
    curl https://hello-world-hello-world.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud
    ```
    {: pre}

    Saída de exemplo:
    ```
    Hello world from hello-world-9cv7d! Seu app está funcionando em um contêiner!
    ```
    {: screen}
6.  **Opcional** Para limpar os recursos que você criou nesta lição, é possível usar os rótulos que são designados a cada app.
    1.  Liste todos os recursos para cada app no projeto `hello-world`.
        ```
        oc get all -l app=hello-world -o name -n hello-world
        ```
        {: pre}
        Saída de exemplo:
        ```
        pod/hello-world-1-dh2ff
        replicationcontroller/hello-world-1
        service/hello-world
        deploymentconfig.apps.openshift.io/hello-world
        buildconfig.build.openshift.io/hello-world
        build.build.openshift.io/hello-world-1
        imagestream.image.openshift.io/hello-world
        imagestream.image.openshift.io/node
        route.route.openshift.io/hello-world
        ```
        {: screen}
    2.  Exclua todos os recursos que você criou.
        ```
        oc delete all -l app=hello-world -n hello-world
        ```
        {: pre}



<br />


## O que Vem a Seguir?
{: #openshift_next}

Para obter mais informações sobre como trabalhar com seus apps e serviços de roteamento, consulte o [Developer Guide do OpenShift](https://docs.openshift.com/container-platform/3.11/dev_guide/index.html).

Instale dois complementos populares do {{site.data.keyword.containerlong_notm}}: o [{{site.data.keyword.la_full_notm}}](/docs/openshift?topic=openshift-openshift_health#openshift_logdna) e o [{{site.data.keyword.mon_full_notm}}](/docs/openshift?topic=openshift-openshift_health#openshift_sysdig).
