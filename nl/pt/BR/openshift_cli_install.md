---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, oc

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

# Instalando a CLI do Red Hat OpenShift Container Platform
{: #openshift-cli}

É possível usar o alias de plug-in da CLI do {{site.data.keyword.containerlong}} para o OpenShift (`ibmcloud oc`) para criar e gerenciar sua infraestrutura de cluster do OpenShift, como a criação de clusters e de nós do trabalhador. Em seguida, é possível usar a CLI do OpenShift Origin (`oc`) para gerenciar os recursos dentro do seu cluster do OpenShift, como projetos, pods e implementações. 

## Instalando a CLI e os plug-ins do IBM Cloud
{: #cli_ibmcloud_oc}

Consulte o tópico nos [docs do {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps) para instalar as CLIs a seguir.
{: shortdesc}

* {{site.data.keyword.cloud_notm}}  CLI (` ibmcloud `)
* Plug-in do {{site.data.keyword.containershort_notm}} (alias `ibmcloud oc` para clusters do OpenShift)
* Plug-in do Container Registry (`ibmcloud cr`)

<br />


## Instalando a CLI do OpenShift Origin (`oc`)
{: #cli_oc}

Para visualizar uma versão local do painel do OpenShift e para implementar apps em seus clusters do Red Hat OpenShift on IBM Cloud, instale a CLI do OpenShift Origin (`oc`). A CLI `oc` inclui uma versão correspondente da CLI do Kubernetes (`kubectl`). Para obter mais informações, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/cli_reference/get_started_cli.html).
{: shortdesc}

Usando tanto o cluster Kubernetes da comunidade quanto do OpenShift? A CLI `oc` é fornecida com os binários `oc` e `kubectl`, mas seus diferentes clusters podem executar diferentes versões do Kubernetes, como 1.11 no OpenShift e 1.13.8 no Ubuntu. Certifique-se de usar o binário `kubectl` que corresponde à versão do Kubernetes `major.minor` do cluster.
{: note}

1.  [Faça download da CLI do OpenShift Origin ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.okd.io/download.html) para seu sistema operacional local e versão do OpenShift. A versão padrão do OpenShift atual é 3.11.

2.  Se você usar Mac OS ou Linux, conclua as etapas a seguir para incluir os binários em sua variável do sistema `PATH`. Se você usar o Windows, instale a CLI `oc` no mesmo diretório que a CLI do {{site.data.keyword.cloud_notm}}. Essa configuração economiza algumas mudanças de caminho de arquivo ao executar comandos posteriormente.
    1.  Mova os arquivos executáveis `oc` e `kubectl` para o diretório `/usr/local/bin`.
        ```
        mv /<filepath>/oc /usr/local/bin/oc && mv /<filepath>/kubectl /usr/local/bin/kubectl
        ```
        {: pre}

    2.  Certifique-se de que `/usr/local/bin` esteja listado na variável do sistema `PATH`. A variável `PATH` contém todos os diretórios nos quais o sistema operacional pode localizar arquivos executáveis. Os diretórios que estão listados na variável `PATH` servem propósitos diferentes. `/usr/local/bin` é usado para armazenar arquivos executáveis para o software que não faz parte do sistema operacional e que foi instalado manualmente pelo administrador do sistema.
        ```
        echo $PATH
        ```
        {: pre}
        Exemplo de saída da CLI:
        ```
        /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
        ```
        {: screen}
3.  Se você tiver clusters que executam diferentes versões do Kubernetes, como um cluster do OpenShift com a versão 1.11 e um cluster Kubernetes da comunidade com a versão 1.15.1, faça download de cada arquivo binário de versão de `kubectl` em um diretório separado.
    1.  Exclua o arquivo binário `kubectl` que é fornecido com a instalação `oc`, pois essa versão de `kubectl` não funciona com clusters Kubernetes da comunidade.
        ```
        rm /usr/local/bin/kubectl
        ```
        {: pre}
    2.  [Faça download de arquivos binários `kubectl` separados](/docs/containers?topic=containers-cs_cli_install#kubectl) que correspondam às versões de seus clusters do OpenShift e do Kubernetes da comunidade.
    3.  **Opcional**: configure um alias em seu perfil de terminal local para apontar binários separados que correspondam à versão de `kubectl` de que seu cluster precisa.
4.  **Opcional**: [ative a conclusão automática para comandos `kubectl` ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion). As etapas variam, dependendo do shell usado. É possível repetir as etapas para ativar a conclusão automática para comandos `oc`. Por exemplo, em bash no Linux, em vez de `kubectl completion bash >/etc/bash_completion.d/kubectl`, é possível executar `oc completion bash >/etc/bash_completion.d/oc_completion`.

Em seguida, comece a [Criação de um cluster do Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-openshift_tutorial).

Para obter mais informações sobre a CLI do OpenShift Origin, consulte os [docs de comandos `oc` ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/cli_reference/basic_cli_operations.html).
{: note}


<br />


## Acessando um cluster do OpenShift por meio do terminal ou de ferramentas de automação
{: #openshift_cluster_login}

O Red Hat OpenShift on IBM Cloud é integrado ao {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Com o IAM, é possível autenticar usuários e serviços usando suas identidades do IAM e autorizar ações com funções de acesso e políticas. Ao se autenticar como um usuário por meio do console do OpenShift, sua identidade do IAM é usada para gerar um token de login do OpenShift que pode ser usado para efetuar login no terminal. É possível automatizar a criação de log em seu cluster criando uma chave de API do IAM para usar para o comando `oc login`.
{:shortdesc}

** Antes de iniciar **:
* [Instale a CLI `oc`](#cli_oc).
* [Criar um cluster do OpenShift](/docs/openshift?topic=openshift-openshift-create-cluster).
* Verifique se seu cluster está em um estado funcional executando `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>`. Se seu cluster não estiver em um estado funcional, revise o guia [Depurando clusters](/docs/containers?topic=containers-cs_troubleshoot) para obter ajuda. Por exemplo, se o seu cluster for provisionado em uma conta protegida por um dispositivo de gateway de firewall, você deverá [definir as configurações do firewall para permitir o tráfego de saída para as portas e endereços IP apropriados](/docs/openshift?topic=containers-firewall).

**Para efetuar login em seu cluster como um usuário por meio do terminal**:
1.  No [console do {{site.data.keyword.containerlong_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift), clique no cluster que deseja acessar.
2.  Clique na guia **Acessar** e siga as instruções.

<br>
**Para automatizar o acesso ao seu cluster com uma chave de API**:
1.  Crie uma chave de API do {{site.data.keyword.cloud_notm}}.<p class="important">Salve sua chave de API em um local seguro. Não é possível recuperar a chave de API novamente. Se desejar exportar a saída para um arquivo em sua máquina local, inclua a sinalização `--file <path>/<file_name>`.</p>
    ```
    ibmcloud iam api-key-create <name>
    ```
    {: pre}
2.  Obtenha a **URL principal** do cluster que deseja acessar.
    ```
    ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
    ```
    {: pre}
3.  Use a chave de API e a URL do cluster para efetuar login em seu cluster do OpenShift. O nome do usuário (`-u`) é `apikey`, a senha (`-p`) é seu valor de chave de API e o `--server` é a URL do cluster mestre.
    ```
    oc login -u apikey -p <API_key> --server=<master_URL>
    ```
    {: pre}

    Também é possível usar uma chamada de API para trocar suas credenciais do {{site.data.keyword.cloud_notm}} IAM para um token do OpenShift. Para obter mais informações, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/architecture/additional_concepts/authentication.html#obtaining-oauth-tokens).

    Solicitação curl de exemplo:
    ```
    curl -u 'apikey:<API_key>' -H "X-CSRF-Token: a" 'https://<master_URL>:<port>/oauth/authorize?client_id=openshift-challenging-client&response_type=token' -vvv
    ```
    {: pre}


