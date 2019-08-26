---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, clusters

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

# Criando clusters do OpenShift
{: #openshift-create-cluster}

Crie um cluster do {{site.data.keyword.openshiftlong}} no {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

## Pré-requisitos
{: #openshift_cluster_prereqs}

Para criar clusters do OpenShift, conclua as etapas de pré-requisito a seguir.

1.  [Prepare sua conta para criar clusters](/docs/containers?topic=containers-clusters#cluster_prepare). Essa etapa inclui a criação de uma conta faturável, a configuração de uma chave de API com permissões de infraestrutura, a garantia de ter acesso de Administrador no {{site.data.keyword.cloud_notm}} IAM, o planejamento de grupos de recursos e a configuração de rede de conta.
2.  [Prepare-se para criar clusters](/docs/containers?topic=containers-clusters#prepare_cluster_level). Essa etapa inclui planejar a configuração do cluster, estimar custos e, se aplicável, permitir o tráfego de rede por meio de um firewall.<p class="note">Os clusters do OpenShift estão disponíveis [somente como um cluster padrão, não grátis](/docs/openshift?topic=openshift-faqs#openshift_free).</p>
3.   [Instale as CLIs do {{site.data.keyword.cloud_notm}} e do OpenShift](/docs/openshift?topic=openshift-openshift-cli).

<br />


## Criando um cluster com o console
{: #openshift_create_cluster_console}

Crie um cluster padrão do OpenShift no console do {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

Antes de iniciar, [conclua os pré-requisitos](#openshift_cluster_prereqs).

1.  Crie um cluster.
    1.  Efetue login em sua [conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/).
    2.  No menu hambúrguer ![Ícone de menu hambúrguer](../icons/icon_hamburger.svg "Ícone de menu hambúrguer"), selecione **OpenShift** e, em seguida, clique em **Criar cluster**.
    3.  Escolha os detalhes e o nome da configuração do cluster.
    *   Preencha o nome do cluster, o grupo de recursos e tags.
    *   Para a **Localização**, configure a **Geografia** e, em seguida, selecione qualquer uma das seis [Localizações](/docs/openshift?topic=openshift-regions-and-zones) **metropolitanas** de várias zonas mundiais para usar para suas **Zonas do trabalhador**.
    *   Para o **Conjunto de trabalhadores padrão**, escolha um tipo disponível para seus nós do trabalhador. O Red Hat OpenShift on IBM Cloud suporta o OpenShift versão 3.11 somente, o que inclui o Kubernetes versão 1.11. O sistema operacional é o Red Hat Enterprise Linux 7.

    1.  Para concluir, clique em **Criar cluster**.<p class="note">A criação do cluster pode levar algum tempo para ser concluída. Depois que o estado do cluster mostra **Normal**, a rede de cluster e os componentes de balanceamento de carga levam mais de 10 minutos para implementar e atualizar o domínio do cluster usado para o console da web do OpenShift e outras rotas. Aguarde até que o cluster esteja pronto antes de continuar com a próxima etapa, verificando se o **Subdomínio do Ingress** segue um padrão de `<cluster_name>.<region>.containers.appdomain.cloud`.<br><br>Se seu cluster não atingir o estado **implementado**, confira o guia [Depurando clusters](/docs/containers?topic=containers-cs_troubleshoot) para obter ajuda. Por exemplo, se o seu cluster for provisionado em uma conta protegida por um dispositivo de gateway de firewall, você deverá [definir as configurações do firewall para permitir o tráfego de saída para as portas e endereços IP apropriados](/docs/openshift?topic=containers-firewall).</p>
2.  Na página de detalhes do cluster, clique em **Console da web do OpenShift**. Para obter mais informações sobre o uso do console do OpenShift, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html).
3.  Para continuar a trabalhar no terminal: na barra de menus do console da web do OpenShift, clique em seu perfil **IAM#user.name@email.com > Copiar comando de login**. Cole o comando de login `oc` copiado em seu terminal para autenticar por meio da CLI.

<br />


## Criando um cluster com a CLI
{: #openshift_create_cluster_cli}

Crie um cluster padrão do OpenShift usando a CLI do {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Antes de iniciar, [conclua os pré-requisitos](#openshift_cluster_prereqs).

1.  Efetue login na conta que você configurou para criar clusters do OpenShift. Tenha como destino a região **us-east** ou **eu-gb** e o grupo de recursos. Se você tiver uma conta federada, inclua a sinalização `--sso`.
    ```
    ibmcloud login -r (us-east|eu-gb) [-g default] [--sso]
    ```
    {: pre}
2.  Crie um cluster.
    ```
    ibmcloud oc cluster-create --name <name> --location <zone> --kube-version <openshift_version> --machine-type <worker_node_flavor> --workers <number_of_worker_nodes_per_zone> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    Comando de exemplo para criar um cluster com os três nós do trabalhador que possuem quatro núcleos e 16 GB de memória em Washington, DC:

    ```
    ibmcloud oc cluster-create --name my_openshift --location wdc04 --kube-version 3.11_openshift --machine-type b3c.4x16.encrypted  --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    <table summary="A primeira linha na tabela abrange ambas as colunas. O restante das linhas deve ser lido da esquerda para a direita, com o componente de comando na coluna um e a descrição correspondente na coluna dois.">
    <caption>Os componentes de criação de cluster</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Ícone de ideia"/> entendendo os componentes desse comando</th>
    </thead>
    <tbody>
    <tr>
    <td><code>cluster-create</code></td>
    <td>O comando para criar um cluster de infraestrutura clássica em sua conta do {{site.data.keyword.cloud_notm}}.</td>
    </tr>
    <tr>
    <td><code>--name <em>&lt;name&gt;</em></code></td>
    <td>Insira um nome para seu cluster. O nome deve iniciar com uma letra, pode conter letras, números e hifens (-) e deve ter 35 caracteres ou menos. Use um nome que seja exclusivo em regiões do {{site.data.keyword.cloud_notm}}.</td>
    </tr>
    <tr>
    <td><code>--location <em>&lt;zone&gt;</em></code></td>
    <td>Especifique a zona na qual você deseja criar seu cluster. Para obter uma lista de zonas suportadas, consulte [Locais de várias zonas](/docs/openshift?topic=openshift-regions-and-zones#zones).</p></td>
    </tr>
    <tr>
      <td><code>--kube-version <em>&lt;openshift_version&gt;</em></code></td>
      <td>Deve-se escolher uma versão suportada do OpenShift. As versões do OpenShift incluem uma versão do Kubernetes que difere das versões do Kubernetes disponíveis nos clusters do Ubuntu do Kubernetes da comunidade. Para listar as versões do OpenShift disponíveis, execute `ibmcloud oc versions`. Para criar um cluster com a versão de correção mais recente, é possível especificar apenas a versão principal e secundária, tal como ` 3.11_openshift`.<br><br>O Red Hat OpenShift on IBM Cloud suporta o OpenShift versão 3.11 somente, o que inclui o Kubernetes versão 1.11. O sistema operacional é o Red Hat Enterprise Linux 7.
</td>
    </tr>
    <tr>
    <td><code>--machine-type <em>&lt;worker_node_flavor&gt;</em></code></td>
    <td>Escolha um tipo de máquina, ou tipo, para os nós do trabalhador. É possível implementar os nós do trabalhador como máquinas virtuais em hardware compartilhado ou dedicado ou como máquinas físicas no bare metal. Os tipos de máquinas físicas e virtuais disponíveis variam de acordo com a zona na qual você implementa o cluster. Para listar os tipos disponíveis, execute `ibmcloud oc flavors --zone <zone>`.</td>
    </tr>
    <tr>
    <td><code>--workers <em>&lt;number_of_worker_nodes_per_zone&gt;</em></code></td>
    <td>O número de nós do trabalhador a serem incluídos no cluster. Você pode desejar especificar pelo menos três nós do trabalhador para que seu cluster tenha recursos suficientes para executar os componentes padrão e para alta disponibilidade. Se a opção <code>--workers</code> não for especificada, um nó do trabalhador será criado.</td>
    </tr>
    <tr>
    <td><code>--public-vlan <em>&lt;public_vlan_id&gt;</em></code></td>
    <td>Se você já tiver uma VLAN pública configurada em sua conta da infraestrutura do IBM Cloud para essa zona, insira o ID da VLAN pública. Para verificar VLANs disponíveis, execute `ibmcloud oc vlans --zone <zone>`. <br><br>Se você não tiver uma VLAN pública em sua conta, não especifique essa opção. O {{site.data.keyword.containerlong_notm}} cria automaticamente uma VLAN pública para você.</td>
    </tr>
    <tr>
    <td><code>--private-vlan <em>&lt;private_vlan_id&gt;</em></code></td>
    <td>Se você já tiver uma VLAN privada configurada em sua conta de infraestrutura do IBM Cloud para essa zona, insira o ID da VLAN privada. Para verificar VLANs disponíveis, execute `ibmcloud oc vlans --zone <zone>`. <br><br>Se você não tem uma VLAN privada em sua conta, não especifique esta opção. O {{site.data.keyword.containerlong_notm}} cria automaticamente uma VLAN privada para você.</td>
    </tr>
    </tbody></table>
3.  Liste os detalhes do cluster. Revise o **Estado** do cluster, verifique o **Subdomínio do Ingress** e anote a **URL principal**.<p class="note">A criação do cluster pode levar algum tempo para ser concluída. Depois que o estado do cluster mostra **Normal**, a rede de cluster e os componentes de balanceamento de carga levam mais de 10 minutos para implementar e atualizar o domínio do cluster usado para o console da web do OpenShift e outras rotas. Aguarde até que o cluster esteja pronto antes de continuar com a próxima etapa, verificando se o **Subdomínio do Ingress** segue um padrão de `<cluster_name>.<region>.containers.appdomain.cloud`.<br><br>Seu cluster não está em um estado **implementado**? Consulte o guia [Clusters de depuração](/docs/containers?topic=containers-cs_troubleshoot) para obter ajuda. Por exemplo, se o seu cluster for provisionado em uma conta protegida por um dispositivo de gateway de firewall, você deverá [definir as configurações do firewall para permitir o tráfego de saída para as portas e endereços IP apropriados](/docs/openshift?topic=containers-firewall).</p>

    ```
    ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
    ```
    {: pre}

4.  Faça download dos arquivos de configuração para se conectar ao seu cluster.
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
5.  Em seu navegador, navegue para o endereço de sua **URL principal** e anexe `/console`. Por exemplo, `https://c0.containers.cloud.ibm.com:23652/console`.
6.  Na barra de menus do console da web do OpenShift, clique em seu perfil **IAM#user.name@email.com > Copiar comando de login**. Cole o comando de login `oc` copiado em seu terminal para autenticar por meio da CLI.<p class="tip">Salve a URL do cluster principal para acessar o console do OpenShift posteriormente. Em sessões futuras, será possível ignorar a etapa `cluster-config` e copiar o comando de login por meio do console.</p>
7.  Verifique se os comandos `oc` são executados corretamente com seu cluster verificando a versão.

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

<br />


## Próximas etapas
{: #next_steps}

Quando o cluster estiver funcionando, será possível verificar as tarefas a seguir:
- Se você criou o cluster em uma zona com capacidade para multizona, [difunda os nós do trabalhador incluindo uma zona em seu cluster](/docs/openshift?topic=containers-add_workers).
- [Implemente um app em seu cluster](/docs/containers?topic=openshift-openshift_apps).
- [Exponha seus apps com rotas](/docs/openshift?topic=openshift-openshift_routes).
