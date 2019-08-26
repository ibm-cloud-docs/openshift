---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, rhoks, roks, rhos, ibmcloud, ic, oc, ibmcloud oc

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

# CLI do Red Hat OpenShift on IBM Cloud
{: #kubernetes-service-cli}

Consulte esses comandos para criar e gerenciar **clusters OpenShift ou Kubernetes da comunidade** no {{site.data.keyword.containerlong}}.
{:shortdesc}

* **Comunidade do Kubernetes**: [Instalar o plug-in da CLI](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps), que usa o alias `ibmcloud ks`.
* **OpenShift**: [Instalar o plug-in da CLI](/docs/openshift?topic=openshift-openshift-cli), que usa o alias `ibmcloud oc`.

No terminal, você é notificado quando atualizações para a CLI `ibmcloud` e plug-ins estão disponíveis. Certifique-se de manter sua CLI atualizada para que seja possível usar todos os comandos e sinalizações disponíveis.

Procurando comandos `ibmcloud cr`? Consulte a [Referência da CLI do {{site.data.keyword.registryshort_notm}}](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli). Procurando comandos `kubectl`? Consulte a [documentação de Kubernetes
![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubectl.docs.kubernetes.io/).
{:tip}

## Usando o plug-in beta do {{site.data.keyword.containerlong_notm}}
{: #cs_beta}

Uma versão reprojetada do plug-in do {{site.data.keyword.containerlong_notm}} está disponível como um beta. O plug-in do {{site.data.keyword.containerlong_notm}} reprojetado agrupa comandos em categorias e muda os comandos de uma estrutura hifenizada para uma estrutura espaçada. Além disso, iniciando com a versão beta `0.3` (padrão), a nova [funcionalidade de terminal global](/docs/containers?topic=containers-regions-and-zones#endpoint) está disponível.
{: shortdesc}

As seguintes versões beta do plug-in do {{site.data.keyword.containerlong_notm}} reprojetado estão disponíveis.
* O comportamento padrão é `0.3`. Assegure-se de que seu plug-in do {{site.data.keyword.containerlong_notm}} use a versão `0.3` mais recente, executando `ibmcloud plugin update kubernetes-service`.
* Para usar `0.4` ou `1.0`, configure a variável de ambiente `IKS_BETA_VERSION` para a versão beta que você deseja usar:
    ```
    export IKS_BETA_VERSION= < beta_version>
    ```
    {: pre}
* Para usar a funcionalidade de terminal regional descontinuada, tenha como destino o terminal regional com o [comando `init`](#cs_init).
    ```
    ibmcloud oc init --host <regional_endpoint>
    ```
    {: pre}

</br>

<table>
<caption>Versões Beta do plug-in {{site.data.keyword.containerlong_notm}} reprojetado</caption>
  <thead>
    <th>Versão Beta</th>
    <th>Estrutura de saída `ibmcloud oc help`</th>
    <th>Estrutura de comando</th>
    <th>Funcionalidade de local</th>
  </thead>
  <tbody>
    <tr>
      <td><code>0.2</code> (descontinuado)</td>
      <td>Anterior: os comandos são mostrados na estrutura hifenizada e são listados alfabeticamente.</td>
      <td>Anterior e beta: é possível executar comandos na estrutura hifenizada anterior (`ibmcloud oc alb-cert-get`) ou na estrutura espaçada beta (`ibmcloud oc alb cert get`).</td>
      <td>Regional: [tenha uma região como destino e use um terminal regional para trabalhar com recursos nessa região](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
    <tr>
      <td><code>0.3</code> (padrão)</td>
      <td>Anterior: os comandos são mostrados na estrutura hifenizada e são listados alfabeticamente.</td>
      <td>Anterior e beta: é possível executar comandos na estrutura hifenizada anterior (`ibmcloud oc alb-cert-get`) ou na estrutura espaçada beta (`ibmcloud oc alb cert get`).</td>
      <td>Global: [Use o terminal global para trabalhar com recursos em qualquer localização](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
    <tr>
      <td><code>0.4</code></td>
      <td>Beta: os comandos são mostrados na estrutura espaçada e são listados em categorias.</td>
      <td>Anterior e beta: é possível executar comandos na estrutura hifenizada anterior (`ibmcloud oc alb-cert-get`) ou na estrutura espaçada beta (`ibmcloud oc alb cert get`).</td>
      <td>Global: [Use o terminal global para trabalhar com recursos em qualquer localização](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
    <tr>
      <td><code> 1.0 </code></td>
      <td>Beta: os comandos são mostrados na estrutura espaçada e são listados em categorias.</td>
      <td>Beta: é possível executar comandos somente na estrutura espaçada beta (`ibmcloud oc alb cert get`).</td>
      <td>Global: [Use o terminal global para trabalhar com recursos em qualquer localização](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
  </tbody>
</table>



<br />


## Comandos de API
{: #api_commands}

### `ibmcloud oc api`
{: #cs_cli_api}

Destine o terminal da API para o {{site.data.keyword.containerlong_notm}}. Se você não especificar um terminal, será possível visualizar informações sobre o terminal atual que está destinado.
{: shortdesc}

Os terminais específicos da região foram descontinuados. Em vez disso, use o [terminal global](/docs/containers?topic=containers-regions-and-zones#endpoint). Se tiver que usar os terminais regionais, [configure a variável de ambiente `IKS_BETA_VERSION` no plug-in do {{site.data.keyword.containerlong_notm}} para `0.2`](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_beta).
{: deprecated}

Se você precisar listar e trabalhar com recursos de apenas uma região, será possível usar o comando `ibmcloud oc api` para ter como destino um terminal regional em vez do terminal global.
* Dallas (Sul dos EUA, us-south): `https://us-south.containers.cloud.ibm.com`
* Frankfurt (UE Central, eu-de): `https://eu-de.containers.cloud.ibm.com`
* Londres (Sul do Reino Unido, eu-gb): `https://eu-gb.containers.cloud.ibm.com`
* Sydney (Sul da Ásia-Pacífico, au-syd): `https://au-syd.containers.cloud.ibm.com`
* Tóquio (Norte da Ásia-Pacífico, jp-tok): `https://jp-tok.containers.cloud.ibm.com`
* Washington, D.C. (Leste dos EUA, us-east): `https://us-east.containers.cloud.ibm.com`

Para usar a funcionalidade global, será possível usar o comando `ibmcloud oc api` novamente para ter o terminal global como destino: `https://containers.cloud.ibm.com`

```
ibmcloud oc api --endpoint ENDPOINT [--insecure] [--skip-ssl-validation] [--api-version VALUE] [-s]
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

**Opções de comando**:
<dl>
<dt><code> -- endpoint  <em> ENDPOINT </em> </code></dt>
  <dd>O terminal da API do  {{site.data.keyword.containerlong_notm}} . <strong>Nota</strong>: esse terminal é diferente dos terminais do {{site.data.keyword.cloud_notm}}. Este valor é necessário para configurar o terminal de API.
   </dd>

<dt><code>-- inseguro</code></dt>
<dd>Permitir uma conexão HTTP insegura. Este sinalizador é opcional.</dd>

<dt><code>--validation-skip-ssl</code></dt>
<dd>Permitir certificados SSL insegura. Este sinalizador é opcional.</dd>

<dt><code>-- api-version VALUE</code></dt>
<dd>Especifique a versão da API do serviço que você deseja usar. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>

</dl>

**Exemplo**: visualize informações sobre o terminal de API atual que é destinado.
```
ibmcloud oc api
```
{: pre}

```
API Endpoint:          https://containers.cloud.ibm.com
API Version:           v1
Skip SSL Validation:   false
Region:                us-south
```
{: screen}

</br>
### `ibmcloud oc apiserver-refresh (cluster-refresh)`
{: #cs_apiserver_refresh}

Aplique as mudanças de configuração para o mestre do Kubernetes que são solicitadas com os comandos `ibmcloud oc apiserver-config-set`, `apiserver-config-unset`, `cluster-feature-enable` ou `cluster-feature-disable`. Os componentes do principal do Kubernetes altamente disponíveis são reiniciados em uma reinicialização contínua. Os nós do trabalhador, os apps e os recursos não são modificados e continuam a ser executados.
{: shortdesc}



```
ibmcloud oc apiserver-refresh --cluster CLUSTER [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

<br />


## Comandos de uso do plug-in da CLI
{: #cli_plug-in_commands}

### `ibmcloud oc help`
{: #cs_help}

Visualizar uma lista de comandos e parâmetros suportados.
{: shortdesc}

```
ibmcloud oc help
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

** Opções de comando **: Nenhuma

</br>
### `ibmcloud oc init`
{: #cs_init}

Inicialize o plug-in do {{site.data.keyword.containerlong_notm}} ou especifique a região em que você deseja criar ou acessar clusters do Kubernetes.
{: shortdesc}

Os terminais específicos da região foram descontinuados. Em vez disso, use o [terminal global](/docs/containers?topic=containers-regions-and-zones#endpoint). Se tiver que usar os terminais regionais, [configure a variável de ambiente `IKS_BETA_VERSION` no plug-in do {{site.data.keyword.containerlong_notm}} para `0.2`](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_beta).
{: deprecated}

Se você precisar listar e trabalhar com recursos de uma região apenas, será possível usar o comando `ibmcloud oc init` para ter como destino um terminal regional em vez do terminal global.

* Dallas (Sul dos EUA, us-south): `https://us-south.containers.cloud.ibm.com`
* Frankfurt (UE Central, eu-de): `https://eu-de.containers.cloud.ibm.com`
* Londres (Sul do Reino Unido, eu-gb): `https://eu-gb.containers.cloud.ibm.com`
* Sydney (Sul da Ásia-Pacífico, au-syd): `https://au-syd.containers.cloud.ibm.com`
* Tóquio (Norte da Ásia-Pacífico, jp-tok): `https://jp-tok.containers.cloud.ibm.com`
* Washington, D.C. (Leste dos EUA, us-east): `https://us-east.containers.cloud.ibm.com`

Para usar a funcionalidade global, é possível usar o comando `ibmcloud oc init` novamente para ter o terminal global como destino: `https://containers.cloud.ibm.com`

```
ibmcloud oc init [--host HOST] [--insecure] [-p] [-u] [-s]
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

**Opções de comando**:
<dl>
<dt><code>--host <em>HOST</em></code></dt>
<dd>O  {{site.data.keyword.containerlong_notm}}  terminal de API a ser usado. Esse valor é opcional.</dd>

<dt><code>-- inseguro</code></dt>
<dd>Permitir uma conexão HTTP insegura.</dd>

<dt><code>-p</code></dt>
<dd>Sua senha do IBM Cloud.</dd>

<dt><code>-u</code></dt>
<dd>O IBM Cloud username.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>

</dl>

**Exemplos**:
*  Exemplo para que o terminal regional do Sul dos EUA seja o destino:
  ```
  ibmcloud oc init --host https://us-south.containers.cloud.ibm.com
  ```
  {: pre}
*  Exemplo para destinar o terminal global novamente:
  ```
  ibmcloud oc init --host https://containers.cloud.ibm.com
  ```
  {: pre}
</br>

### `ibmcloud oc messages`
{: #cs_messages}

Visualize as mensagens atuais por meio do plug-in da CLI do {{site.data.keyword.containerlong_notm}} para o usuário IBMid.
{: shortdesc}

```
ibmcloud oc messages
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

<br />


## Comandos do cluster: gerenciamento
{: #cluster_mgmt_commands}

### `ibmcloud oc addon-versions`
{: #cs_addon_versions}

Visualize uma lista de versões suportadas para complementos gerenciados no {{site.data.keyword.containerlong_notm}}.
{: shortdesc}



```
ibmcloud oc addon-versions [--addon ADD-ON_NAME] [--json] [-s]
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

**Opções de comando**:
<dl>
<dt><code>--addon <em>ADD-ON_NAME</em></code></dt>
<dd>Opcional: especifique um nome de complemento, como <code>istio</code> ou <code>knative</code>, para o qual filtrar versões.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:

  ```
  ibmcloud oc addon-versions --addon istio
  ```
  {: pre}

</br>
### `ibmcloud oc cluster-addon-disable`
{: #cs_cluster_addon_disable}

Desativar um complemento gerenciado em um cluster existente. Esse comando deve ser combinado com um dos subcomandos a seguir para o complemento gerenciado que você deseja desativar.
{: shortdesc}





#### `ibmcloud oc cluster-addon-disable istio`
{: #cs_cluster_addon_disable_istio}

Desativar o complemento Istio gerenciado. Remove todos os componentes principais do Istio do cluster, incluindo o Prometheus.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable istio --cluster CLUSTER [-f]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>-f</code></dt>
<dd>Opcional: esse complemento do Istio é uma dependência para os complementos gerenciados <code>istio-extras</code>, <code>istio-sample-bookinfo</code> e <code>knative</code>. Inclua esse sinalizador para também desativar esses complementos.</dd>
</dl>

#### `ibmcloud oc cluster-addon-disable istio-extras`
{: #cs_cluster_addon_disable_istio_extras}

Desative o Istio extras add-on gerenciado. Remove o Grafana, o Jeager e o Kiali do cluster.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable istio-extras --cluster CLUSTER [-f]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>-f</code></dt>
<dd>Opcional: esse complemento do Istio é uma dependência para o complemento gerenciado <code>istio-sample-bookinfo</code>. Inclua essa sinalização para também desativar esse complemento.</dd>
</dl>

#### `ibmcloud oc cluster-addon-disable istio-sample-bookinfo`
{: #cs_cluster_addon_disable_istio_sample_bookinfo}

Desative o complemento do Istio BookInfo gerenciado. Remove do cluster todas as implementações, os pods e outros recursos do aplicativo BookInfo.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable istio-sample-bookinfo --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>
</dl>

#### `ibmcloud oc cluster-addon-disable knative`
{: #cs_cluster_addon_disable_knative}

Desative o complemento Knative gerenciado para remover a estrutura Knative sem servidor do cluster.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable knative --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>
</dl>

#### `ibmcloud oc cluster-addon-disable kube-terminal`
{: #cs_cluster_addon_disable_kube-terminal}

Desative o complemento do [Terminal do Kubernetes](/docs/containers?topic=containers-cs_cli_install#cli_web). Para usar o Terminal do Kubernetes no console do cluster do {{site.data.keyword.containerlong_notm}}, deve-se primeiro ativar o complemento novamente.
{: shortdesc}

```
ibmcloud oc cluster-addon-disable kube-terminal --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>
</dl>

</br>

### `ibmcloud oc cluster-addon-enable`
{: #cs_cluster_addon_enable}

Ative um complemento gerenciado em um cluster existente. Esse comando deve ser combinado com um dos subcomandos a seguir para o complemento gerenciado que você deseja ativar.
{: shortdesc}





#### `ibmcloud oc cluster-addon-enable istio`
{: #cs_cluster_addon_enable_istio}

Ative o  [ Complemento Istio ](/docs/containers?topic=containers-istio) gerenciado. Instala os componentes principais do Istio, incluindo o Prometheus.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable istio --cluster CLUSTER [--version VERSION]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Opcional: especifique a versão do complemento a ser instalado. Se nenhuma versão for especificada, a versão padrão será instalada.</dd>
</dl>

#### `ibmcloud oc cluster-addon-enable istio-extras`
{: #cs_cluster_addon_enable_istio_extras}

Ative o Istio extras extras add-on. Instala o Grafana, o Jeager e o Kiali para fornecer monitoramento, rastreamento e visualização extras para o Istio.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable istio-extras --cluster CLUSTER [--version VERSION] [-y]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Opcional: especifique a versão do complemento a ser instalado. Se nenhuma versão for especificada, a versão padrão será instalada.</dd>

<dt><code> -y </code></dt>
<dd>Opcional: ative a dependência de complementos  <code> istio </code> .</dd>
</dl>

#### `ibmcloud oc cluster-addon-enable istio-sample-bookinfo`
{: #cs_cluster_addon_enable_istio_sample_bookinfo}

Ative o complemento do Istio BookInfo gerenciado. Implementa o [aplicativo de amostra BookInfo para Istio ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://istio.io/docs/examples/bookinfo/) no namespace <code>padrão</code>.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable istio-sample-bookinfo --cluster CLUSTER [--version VERSION] [-y]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Opcional: especifique a versão do complemento a ser instalado. Se nenhuma versão for especificada, a versão padrão será instalada.</dd>

<dt><code> -y </code></dt>
<dd>Opcional: ative as dependências de complemento <code>istio</code> e <code>istio-extras</code>.</dd>
</dl>

#### `ibmcloud oc cluster-addon-enable knative`
{: #cs_cluster_addon_enable_knative}

Ative o [Complemento Knative](/docs/containers?topic=containers-serverless-apps-knative) gerenciado para instalar a estrutura Knative sem servidor.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable knative --cluster CLUSTER [--version VERSION] [-y]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Opcional: especifique a versão do complemento a ser instalado. Se nenhuma versão for especificada, a versão padrão será instalada.</dd>

<dt><code> -y </code></dt>
<dd>Opcional: ative a dependência de complementos  <code> istio </code> .</dd>
</dl>

#### `ibmcloud oc cluster-addon-enable kube-terminal`
{: #cs_cluster_addon_enable_kube-terminal}

Ative o complemento do [Terminal do Kubernetes](/docs/containers?topic=containers-cs_cli_install#cli_web) para usá-lo no console do cluster do {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

```
ibmcloud oc cluster-addon-enable kube-terminal --cluster CLUSTER [--version VERSION]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Opcional: especifique a versão do complemento a ser instalado. Se nenhuma versão for especificada, a versão padrão será instalada.</dd>
</dl>
</br>

### `ibmcloud oc cluster-addons`
{: #cs_cluster_addons}

Listar complementos gerenciados que são ativados em um cluster.
{: shortdesc}



```
ibmcloud oc cluster-addons --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>
</dl>


</br>

### `ibmcloud oc cluster-config`
{: #cs_cluster_config}

Após fazer login, faça download dos dados de configuração e certificados do Kubernetes para se conectar ao seu cluster e executar comandos `oc`. Os arquivos são transferidos por download para `user_home_directory/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>`.
{: shortdesc}



```
ibmcloud oc cluster-config --cluster CLUSTER [--admin] [--export] [--network] [--powershell] [--skip-rbac] [-s] [--yaml]
```
{: pre}

Funções de serviço **Permissões mínimas necessárias**: **Visualizador** ou **Leitor** do {{site.data.keyword.cloud_notm}} IAM para o cluster em {{site.data.keyword.containerlong_notm}}. Além disso, se você tiver apenas uma função da plataforma ou uma função de serviço, restrições adicionais serão aplicadas.
* **Plataforma**: se você tiver apenas uma função da plataforma, será possível executar esse comando, mas você precisará de uma [função de serviço](/docs/containers?topic=containers-users#platform) ou uma [política RBAC customizada](/docs/containers?topic=containers-users#role-binding) para executar ações do Kubernetes no cluster.
* **Serviço**: se você tiver apenas uma função de serviço, será possível executar esse comando. Entretanto, seu administrador de cluster deve fornecer o nome do cluster e o ID porque não é possível executar o comando `ibmcloud oc clusters` ou ativar o console do {{site.data.keyword.containerlong_notm}} para visualizar clusters. Depois de receber o nome do cluster e o ID, é possível [ativar o painel do Kubernetes por meio da CLI](/docs/containers?topic=containers-app#db_cli) e trabalhar com o Kubernetes.

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--admin</code></dt>
<dd>Faça download dos certificados TLS e dos arquivos de permissão para a função de Super usuário. É possível usar os certificados para automatizar tarefas em um cluster sem ter que se autenticar novamente. Os arquivos são transferidos por download para `<user_home_directory>/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>-admin`. Esse valor é opcional.</dd>

<dt><code> -- network </code></dt>
<dd>Faça download do arquivo de configuração do Calico, certificados TLS e arquivos de permissão que são necessários para executar os comandos <code>calicoctl</code> em seu cluster. Esse valor é opcional. **Nota**: para obter o comando de exportação para os dados de configuração e certificados do Kubernetes transferidos por download, deve-se executar esse comando sem essa sinalização.</dd>

<dt><code>--export</code></dt>
<dd>Faça download dos dados de configuração e certificados do Kubernetes sem nenhuma mensagem diferente do comando de exportação. Como nenhuma mensagem é exibida, é possível usar essa sinalização quando você cria scripts automatizados. Esse valor é opcional.</dd>

<dt><code>--powershell</code></dt>
<dd>Recuperar variáveis de ambiente no formato do Windows PowerShell.</dd>

<dt><code> -- skip-rbac </code></dt>
<dd>Ignore a inclusão de funções RBAC do usuário Kubernetes com base nas funções de acesso ao serviço do {{site.data.keyword.cloud_notm}} IAM para a configuração do cluster. Inclua essa opção somente se você [gerenciar suas próprias funções RBAC do Kubernetes](/docs/containers?topic=containers-users#rbac). Se você usar as [funções de acesso ao serviço do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-access_reference#service) para gerenciar todos os usuários do RBAC, não inclua essa opção.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>

<dt><code>--yaml</code></dt>
<dd>Imprime a saída de comando em formato YAML. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-config --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc cluster-create`
{: #cs_cluster_create}

Crie um cluster em sua organização. Para clusters gratuitos, você especifica o nome do cluster; tudo o mais é configurado com um valor padrão. Um cluster grátis é excluído automaticamente após 30 dias. É possível ter um cluster grátis de cada vez. Para aproveitar os recursos integrais do Kubernetes, crie um cluster padrão.
{: shortdesc}



```
ibmcloud oc cluster-create [--file FILE_LOCATION] [--hardware HARDWARE] --zone ZONE --machine-type MACHINE_TYPE --name NAME [--kube-version MAJOR.MINOR.PATCH] [--no-subnet] [--private-vlan PRIVATE_VLAN] [--public-vlan PUBLIC_VLAN] [--private-only] [--private-service-endpoint] [--public-service-endpoint] [--workers WORKER] [--disable-disk-encrypt] [-s]
```
{: pre}

**Permissões mínimas necessárias**:
* Função de plataforma **Administrador** para o {{site.data.keyword.containerlong_notm}} no nível de conta
* Função de plataforma **Administrador** para o {{site.data.keyword.registrylong_notm}} no nível de conta
* Função **Superusuário** para a infraestrutura do IBM Cloud

**Opções de comandos**

<dl>
<dt><code>--file <em>FILE_LOCATION</em></code></dt>

<dd>O caminho para o arquivo YAML para criar seu cluster padrão. Em vez de definir as características de seu cluster usando as opções fornecidas nesse comando, será possível usar um arquivo YAML. Esse valor é opcional para clusters padrão e não está disponível para clusters livres. <p class="note">Se, no comando, você fornecer a mesma opção que o parâmetro no arquivo YAML, o valor no comando terá precedência sobre o valor no YAML. Por exemplo, se você definir um local em seu arquivo YAML e usar a opção <code>--zone</code> no comando, o valor inserido na opção de comando substituirá o valor no arquivo YAML.</p>
<pre class="codeblock">
<code>name: <em>&lt;cluster_name&gt;</em>
zone: <em>&lt;zone&gt;</em>
no-subnet: <em>&lt;no-subnet&gt;</em>
machine-type: <em>&lt;machine_type&gt;</em>
private-vlan: <em>&lt;private_VLAN&gt;</em>
public-vlan: <em>&lt;public_VLAN&gt;</em>
private-service-endpoint: <em>&lt;true&gt;</em>
public-service-endpoint: <em>&lt;true&gt;</em>
hardware: <em>&lt;shared_or_dedicated&gt;</em>
workerNum: <em>&lt;number_workers&gt;</em>
kube-version: <em>&lt;kube-version&gt;</em>
diskEncryption: <em>false</em>
</code></pre>
</dd>

<dt><code>--hardware <em>HARDWARE</em></code></dt>
<dd>O nível de isolamento de hardware para seu nó do trabalhador. Use `dedicated` para que os recursos físicos disponíveis sejam dedicados apenas a você ou `shared` para permitir que recursos físicos sejam compartilhados com outros clientes IBM. O padrão é `shared`. Esse valor é opcional para clusters padrão da VM e não está disponível para clusters grátis. Para os tipos bare metal, especifique `dedicated`.</dd>

<dt><code>--zone <em>ZONE</em></code></dt>
<dd>A zona na qual você deseja criar o cluster. Esse valor é necessário para clusters padrão. Os clusters grátis podem ser criados na região de destino com o comando <code>ibmcloud oc region-set</code>, mas não é possível especificar a zona.

<p>Revise [zonas disponíveis](/docs/containers?topic=containers-regions-and-zones#zones). Para abranger seu cluster entre zonas, deve-se criar o cluster em uma [zona com capacidade para múltiplas zonas](/docs/containers?topic=containers-regions-and-zones#zones).</p>

<p class="note">Quando você seleciona uma zona que está localizada fora de seu país, tenha em mente que você pode requerer autorização legal antes que os dados possam ser armazenados fisicamente em um país estrangeiro.</p>
</dd>

<dt><code>--machine-type <em>MACHINE_TYPE</em></code></dt>
<dd>Escolha um tipo, ou tipo de máquina, para os nós do trabalhador. É possível implementar os nós do trabalhador como máquinas virtuais em hardware compartilhado ou dedicado ou como máquinas físicas no bare metal. Os tipos físicos e virtuais disponíveis variam de acordo com a zona na qual você implementa o cluster. Para obter mais informações, consulte a documentação para o [comando](#cs_machine_types) `ibmcloud oc flavors (machine-types)`. Esse valor é necessário para clusters padrão e não está disponível para clusters livres.</dd>

<dt><code>--name <em>NAME</em></code></dt>
<dd>O nome para o cluster. Este valor é obrigatório. O nome deve iniciar com uma letra, pode conter letras, números e hífen (-) e deve ter 35 caracteres ou menos. Use um nome que seja exclusivo entre as regiões. O nome do cluster e a região na qual o cluster está implementado formam o nome completo do domínio para o subdomínio do Ingress. Para assegurar que o subdomínio do Ingress seja exclusivo dentro de uma região, o nome do cluster pode ser truncado e anexado com um valor aleatório dentro do nome de domínio do Ingress.
</dd>

<dt><code>--kube-version <em>MAJOR.MINOR.PATCH</em></code></dt>
<dd>A versão do Kubernetes para o nó principal do cluster. Esse valor é opcional. Quando a versão não for especificada, o cluster será criado com o padrão de versões do Kubernetes suportadas. Para ver as versões disponíveis, execute <code>ibmcloud oc versions</code>.</dd>

<dt><code>--no-subnet</code></dt>
<dd>Por padrão, uma sub-rede móvel pública e uma privada são criadas na VLAN associada ao cluster. Inclua a sinalização <code>--no-subnet</code> para evitar a criação de sub-redes com o cluster. É possível [criar](#cs_cluster_subnet_create) ou [incluir](#cs_cluster_subnet_add) sub-redes em um cluster posteriormente.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>
<ul>
<li>Esse parâmetro não está disponível para clusters livres.</li>
<li>Se esse cluster padrão for o primeiro cluster padrão que você criar nessa zona, não inclua essa sinalização. Uma VLAN privada é criada para você quando o cluster é criado.</li>
<li>Se você criou um cluster padrão antes dessa zona ou criou uma VLAN privada na infraestrutura do IBM Cloud antes, deverá especificar essa VLAN privada. Os roteadores de VLAN privada sempre iniciam com <code>bcr</code> (roteador de backend) e roteadores de VLAN pública sempre iniciam com <code>fcr</code> (roteador de front-end). Ao criar um cluster e especificar as VLANs públicas e privadas, a combinação de número e letra após esses prefixos devem corresponder.</li>
</ul>
<p>Para descobrir se você já tem uma VLAN privada para uma zona específica ou localizar o nome de uma VLAN privada existente, execute <code>ibmcloud oc vlans --zone <em>&lt;zone&gt;</em></code>.</p></dd>

<dt><code>--public-vlan <em>PUBLIC_VLAN</em></code></dt>
<dd>
<ul>
<li>Esse parâmetro não está disponível para clusters livres.</li>
<li>Se esse cluster padrão for o primeiro cluster padrão que você criar nessa zona, não use essa sinalização. Uma VLAN pública é criada para você quando o cluster é criado.</li>
<li>Se você criou um cluster padrão antes dessa zona ou criou uma VLAN pública na infraestrutura do IBM Cloud antes, especifique essa VLAN pública. Se você deseja conectar seus nós do trabalhador somente a uma VLAN privada, não especifique esta opção. Os roteadores de VLAN privada sempre iniciam com <code>bcr</code> (roteador de backend) e roteadores de VLAN pública sempre iniciam com <code>fcr</code> (roteador de front-end). Ao criar um cluster e especificar as VLANs públicas e privadas, a combinação de número e letra após esses prefixos devem corresponder.</li>
</ul>

<p>Para descobrir se você já tem uma VLAN pública para uma zona específica ou para localizar o nome de uma VLAN pública existente, execute <code>ibmcloud oc vlans --zone <em>&lt;zone&gt;</em></code>.</p></dd>

<dt><code>-- somente privado </code></dt>
<dd>Use essa opção para evitar que uma VLAN pública seja criada. Necessário somente quando você especifica a sinalização `--private-vlan` e não inclui a sinalização `--public-vlan`.<p class="note">Se os nós do trabalhador estão configurados somente com uma VLAN privada, deve-se ativar o terminal em serviço privado ou configurar um dispositivo de gateway. Para obter mais informações, consulte [Comunicação de trabalhador para principal e de usuário para principal](/docs/containers?topic=containers-plan_clusters#workeruser-master).</p></dd>

<dt><code>--private-service-endpoint </code></dt>
<dd>**Clusters padrão que executam Kubernetes versão 1.11 ou mais recente em [Contas ativadas pelo VRF](/docs/resources?topic=resources-private-network-endpoints#getting-started)**: Ative o [terminal em serviço privado](/docs/containers?topic=containers-plan_clusters#workeruser-master) para que o seu mestre Kubernetes e os nós do trabalhador se comuniquem através da VLAN privada. Além disso, é possível escolher ativar o terminal em serviço público usando a sinalização `--public-service-endpoint` para acessar seu cluster por meio da Internet. Se você ativa somente o terminal em serviço privado, deve-se estar conectado à VLAN privada para se comunicar com seu mestre do Kubernetes. Depois de ativar um terminal em serviço privado, não será possível desativá-lo posteriormente.<br><br>Após criar o cluster, é possível obter o terminal executando `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>`.</dd>

<dt><code>--public-service-endpoint </code></dt>
<dd>**Clusters padrão que executam o Kubernetes versão 1.11 ou mais recente**: ative o [terminal de serviço público](/docs/containers?topic=containers-plan_clusters#workeruser-master) para que seu mestre do Kubernetes possa ser acessado pela rede pública, por exemplo, para executar comandos `oc` por meio de seu terminal. Se você tiver uma [conta ativada para VRF](/docs/resources?topic=resources-private-network-endpoints#getting-started) e também incluir a sinalização `--private-service-endpoint`, a comunicação entre o principal e o nó do trabalhador passará pelas redes privada e pública. É possível desativar posteriormente o terminal em serviço público se você desejar um cluster somente privado.<br><br>Após criar o cluster, é possível obter o terminal executando `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>`.</dd>

<dt><code>--workers WORKER</code></dt>
<dd>O número de nós do trabalhador que
você deseja implementar em seu cluster. Se você não especificar essa opção, um cluster com um nó do trabalhador será criado. Esse valor é opcional para clusters padrão e não está disponível para clusters livres.
<p class="important">Se você criar um cluster com somente um nó do trabalhador por zona, poderá ter problemas com o Ingress. Para alta disponibilidade, crie um cluster com pelo menos dois trabalhadores por zona.</br>
</br>Cada nó do trabalhador recebe um ID de nó do trabalhador exclusivo e um nome de domínio que não devem ser mudados manualmente após a criação do cluster. Mudar o ID ou o nome do domínio evita que o mestre do Kubernetes gerencie o cluster.</p></dd>

<dt><code>--disable-disk-encrypt</code></dt>
<dd>Os nós do trabalhador apresentam criptografia de disco AES de 256 bits por padrão; [saiba mais](/docs/containers?topic=containers-security#encrypted_disk). Para desativar a criptografia, inclua essa opção.</dd>
</dl>



**<code>-s</code>**</br>
Não mostrar a mensagem do dia nem atualizar os lembretes. Esse valor é opcional.

**Exemplos**:


**Criar um cluster grátis**: especifique somente o nome do cluster, todo o resto é configurado para um valor padrão. Um cluster grátis é excluído automaticamente após 30 dias. É possível ter um cluster grátis de cada vez. Para aproveitar os recursos integrais do Kubernetes, crie um cluster padrão.

```
ibmcloud oc cluster-create --name my_cluster
```
{: pre}

**Criar o seu primeiro cluster padrão**: o primeiro cluster padrão que é criado em uma zona também cria uma VLAN privada. Portanto, não inclua a sinalização `--public-vlan`.
{: #example_cluster_create}

```
ibmcloud oc cluster-create --zone dal10 --private-vlan my_private_VLAN_ID --machine-type b3c.4x16 --name my_cluster --hardware shared --workers 2
```
{: pre}

**Criar clusters padrão subsequentes**: se você já criou um cluster padrão nessa zona ou criou uma VLAN pública na infraestrutura do IBM Cloud antes, especifique essa VLAN pública com o sinalizador `--public-vlan`. Para descobrir se você já tem uma VLAN pública para uma zona específica ou para localizar o nome de uma VLAN pública existente, execute `ibmcloud oc vlans --zone <zone>`.

```
ibmcloud oc cluster-create --zone dal10 --public-vlan my_public_VLAN_ID --private-vlan my_private_VLAN_ID --machine-type b3c.4x16 --name my_cluster --hardware shared --workers 2
```
{: pre}

</br>

### `ibmcloud oc cluster-feature-disable public-service-endpoint`
{: #cs_cluster_feature_disable}

Desative o terminal em serviço público para um cluster.
{: shortdesc}



**Importante**: antes de desativar o terminal público, deve-se primeiro concluir as etapas a seguir para ativar o terminal em serviço privado:
1. Ative o terminal de serviço privado executando `ibmcloud oc cluster-feature-enable private-service-endpoint --cluster <cluster_name>`.
2. Siga o prompt na CLI para atualizar o servidor de API do mestre do Kubernetes.
3. [Recarregue todos os nós do trabalhador em seu cluster para selecionar a configuração de terminal privado.](#cs_worker_reload)

```
ibmcloud oc cluster-feature-disable public-service-endpoint --cluster CLUSTER [-s] [-f]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-feature-disable public-service-endpoint --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc cluster-feature-enable`
{: #cs_cluster_feature_enable}

Ative um recurso em um cluster existente. Esse comando deve ser combinado com um dos subcomandos a seguir para o recurso que você deseja ativar.
{: shortdesc}



#### `ibmcloud oc cluster-feature-enable private-service-endpoint`
{: #cs_cluster_feature_enable_private_service_endpoint}

Ative o [terminal em serviço privado](/docs/containers?topic=containers-plan_clusters#workeruser-master) para tornar seu cluster principal acessível de forma privada.
{: shortdesc}

Para executar este comando:
1. Ative o [VRF](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) em sua conta de infraestrutura do IBM Cloud. Para verificar se um VRF já está ativado, use o comando `ibmcloud account show`.
2. [Ative sua conta do {{site.data.keyword.cloud_notm}} para usar os terminais em serviço](/docs/resources?topic=resources-private-network-endpoints#getting-started).
3. Execute `ibmcloud oc cluster-feature-enable private-service-endpoint --cluster <cluster_name>`.
4. Siga o prompt na CLI para atualizar o servidor de API do mestre do Kubernetes.
5. [Recarregue todos os nós do trabalhador](#cs_worker_reload) em seu cluster para selecionar a configuração de terminal privado.

```
ibmcloud oc cluster-feature-enable private-service-endpoint --cluster CLUSTER [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-feature-enable private-service-endpoint --cluster my_cluster
```
{: pre}

#### `ibmcloud oc cluster-feature-enable public-service-endpoint`
{: #cs_cluster_feature_enable_public_service_endpoint}

Ative o [terminal em serviço público](/docs/containers?topic=containers-plan_clusters#workeruser-master) para tornar seu cluster principal publicamente acessível.
{: shortdesc}

Após a execução desse comando, deve-se atualizar o servidor de API para usar o terminal de serviço seguindo o prompt na CLI.

```
ibmcloud oc cluster-feature-enable public-service-endpoint --cluster CLUSTER [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-feature-enable public-service-endpoint --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc cluster-get`
{: #cs_cluster_get}

Visualize os detalhes de um cluster.
{: shortdesc}



```
ibmcloud oc cluster-get --cluster CLUSTER [--json] [--showResources] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code><em>--showResources</em></code></dt>
<dd>Mostre mais recursos de cluster, como complementos, VLANs, sub-redes e armazenamento.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-get --cluster my_cluster --showResources
```
{: pre}

**Saída de exemplo**:
```
Name:                           mycluster
ID:                             df253b6025d64944ab99ed63bb4567b6
State:                          normal
Created:                        2018-09-28T15:43:15+0000
Location:                       dal10
Master URL:                     https://c3.<region>.containers.cloud.ibm.com:30426
Public Service Endpoint URL:    https://c3.<region>.containers.cloud.ibm.com:30426
Private Service Endpoint URL:   https://c3-private.<region>.containers.cloud.ibm.com:31140
Master Location:                Dallas
Master Status:                  Ready (21 hours ago)
Ingress Subdomain:              mycluster.us-south.containers.appdomain.cloud
Ingress Secret:                 mycluster
Workers:                        6
Worker Zones:                   dal10, dal12
Version:                        1.11.3_1524
Owner:                          owner@email.com
Resource Group ID:              a8a12accd63b437bbd6d58fb6a462ca7
Resource Group Name:            Default

Subnet VLANs VLAN ID Subnet CIDR Public User-managed 2234947 10.xxx.xx.xxx/29 false false 2234945 169.xx.xxx.xxx/29 true false

```
{: screen}

</br>
### `ibmcloud oc cluster-pull-secret-apply`
{: #cs_cluster_pull_secret_apply}

Crie um ID de serviço do {{site.data.keyword.cloud_notm}} IAM para o cluster, crie uma política para o ID de serviço que designa a função de acesso ao serviço **Leitor** no {{site.data.keyword.registrylong_notm}} e, em seguida, crie uma chave de API para o ID de serviço. A chave de API é, então, armazenada em um `imagePullSecret do Kubernetes` para que seja possível extrair imagens de seus namespaces do {{site.data.keyword.registryshort_notm}} para contêineres que estão no namespace `default` do Kubernetes. Esse processo acontece automaticamente quando você cria um cluster. Se você tiver um erro durante o processo de criação do cluster ou tiver um cluster existente, será possível usar esse comando para aplicar o processo novamente.
{: shortdesc}

Esse método de chave de API substitui o método anterior de autorizar um cluster para acessar o {{site.data.keyword.registrylong_notm}} criando automaticamente um [token](/docs/services/Registry?topic=registry-registry_access#registry_tokens) e armazenando-o em um segredo de extração de imagem. Agora, ao usar as chaves da API do IAM para acessar o {{site.data.keyword.registrylong_notm}}, é possível customizar políticas do IAM para o ID de serviço para restringir o acesso aos seus namespaces ou imagens específicas. Por exemplo, é possível mudar as políticas de ID de serviço no segredo de extração da imagem do cluster para extrair imagens de apenas uma determinada região de registro ou namespace. Antes de poder customizar as políticas do IAM, deve-se [ ativar as políticas do {{site.data.keyword.cloud_notm}} IAM para o {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-user#existing_users).

Para obter mais informações, consulte [Entendendo como seu cluster é autorizado a extrair imagens do {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).



<p class="important">Quando você executa esse comando, a criação de credenciais do IAM e de segredos de extração de imagem é iniciada e pode levar algum tempo para ser concluída. Não será possível implementar contêineres que puxam uma imagem dos domínios `icr.io` do {{site.data.keyword.registrylong_notm}} até que os segredos de extração de imagem sejam criados. Para verificar os segredos de pull de imagem, execute `oc get secrets | grep icr`.</br></br>Se você incluiu políticas do IAM em um ID de serviço existente, como restringir acesso a um registro regional, o ID do serviço, as políticas do IAM e a chave de API para o segredo de pull de imagem serão reconfigurados por esse comando.</p>

```
ibmcloud oc cluster-pull-secret-apply --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**:
*  Função da plataforma **Operador ou Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}
*  Função de plataforma ** Administrador **  no  {{site.data.keyword.registrylong_notm}}

**Opções de comando**:

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>
</dl>

</br>

### `ibmcloud oc cluster-rm`
{: #cs_cluster_rm}

Remover um cluster de sua organização.
{: shortdesc}



```
ibmcloud oc cluster-rm --cluster CLUSTER [--force-delete-storage] [-f] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--force-delete-storage </code></dt>
<dd>Exclui o cluster e qualquer armazenamento persistente usado pelo cluster. **Atenção**: se você incluir essa sinalização, os dados que estiverem armazenados no cluster ou suas instâncias de armazenamento associadas não poderão ser recuperados. Esse valor é opcional.</dd>

<dt><code>-f</code></dt>
<dd>Use essa opção para forçar a remoção de um cluster sem prompts de usuário. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-rm --cluster my_cluster
```
{: pre}

</br>

### `ibmcloud oc cluster-update`
{: #cs_cluster_update}

Atualize o mestre do Kubernetes para a versão de API padrão. Durante a atualização, não é possível acessar nem mudar o cluster. Nós do trabalhador, apps e recursos que foram implementados pelo usuário não são modificados e continuam a ser executados.
{: shortdesc}

Pode ser necessário mudar seus arquivos YAML para implementações futuras. Revise essa [nota sobre a liberação](/docs/containers?topic=containers-cs_versions) para obter detalhes.



```
ibmcloud oc cluster-update --cluster CLUSTER [--kube-version MAJOR.MINOR.PATCH] [--force-update] [-f] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--kube-version <em>MAJOR.MINOR.PATCH</em></code></dt>
<dd>A versão do Kubernetes do cluster. Se você não especificar uma versão, o mestre do Kubernetes será atualizado para a versão de API padrão. Para ver as versões disponíveis, execute [ibmcloud oc kube-versions](#cs_kube_versions). Esse valor é opcional.</dd>

<dt><code>--force-update</code></dt>
<dd>Tente a atualização mesmo se a mudança for maior que duas versões secundárias da versão do nó do trabalhador. Esse valor é opcional.</dd>

<dt><code>-f</code></dt>
<dd>Force o comando a ser executado sem prompts do usuário. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-update --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc clusters`
{: #cs_clusters}

Liste todos os clusters em sua conta do {{site.data.keyword.cloud_notm}}.
{: shortdesc}



Os clusters em todos os locais são retornados. Para filtrar clusters por um local específico, inclua a sinalização `--locations`. Por exemplo, se você filtrar clusters do metro `dal`, serão retornados clusters de diversas zonas nesse metro e clusters de zona única em data centers (zonas) dentro desse metro. Se você filtrar clusters para o data center `dal10` (zona), serão retornados clusters de diversas zonas que tiverem um nó do trabalhador nessa zona e clusters de zona única nessa zona. É possível passar um local ou uma lista de locais separada por vírgulas.

Se você usar a versão beta `0.2` (anterior) do plug-in do {{site.data.keyword.containerlong_notm}}, somente os clusters que estão na região para a qual você está atualmente destinado serão retornados. Para alternar regiões, execute `ibmcloud oc region-set`.
{: deprecated}

```
ibmcloud oc clusters [--locations LOCATION] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--locations <em>LOCATION</em></code></dt>
<dd>Filtre zonas por um local específico ou uma lista de locais separados por vírgula. Para ver as localizações suportadas, execute <code>ibmcloud oc supported-locations</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc clusters --locations ams03,wdc,ap
```
{: pre}

</br>
### Descontinuado: `ibmcloud oc kube-versions`
{: #cs_kube_versions}

Visualize uma lista de versões do Kubernetes suportadas no {{site.data.keyword.containerlong_notm}}. Atualize o seu [cluster mestre](#cs_cluster_update) e [nós do trabalhador](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_update) para a versão padrão para os recursos mais recentes, estáveis.
{: shortdesc}

Esse comando foi descontinuado. Em vez disso, use o [comando `ibmcloud oc versions`](#cs_versions_command).
{: deprecated}

```
ibmcloud oc kube-versions [--json] [-s]
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

**Opções de comando**:
<dl>
<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc kube-versions
```
{: pre}

</br>

### `ibmcloud oc versions`
{: #cs_versions_command}

Liste todas as versões da plataforma de contêineres que estão disponíveis para os clusters do {{site.data.keyword.containerlong_notm}}. Atualize o seu [cluster mestre](#cs_cluster_update) e [nós do trabalhador](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_update) para a versão padrão para os recursos mais recentes, estáveis.
{: shortdesc}



```
ibmcloud oc versions [--show-version PLATFORM][--json] [-s]
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

**Opções de comando**:
<dl>
<dt><code>--show-version</code> <em>PLATFORM</em></dt>
<dd>Mostre somente as versões para a plataforma de contêineres especificada. Os valores suportados são <code>kubernetes</code> ou <code>openshift</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc versions
```
{: pre}

<br />



## Comandos do cluster: serviços e integrações
{: #cluster_services_commands}

### `ibmcloud oc cluster-service-bind`
{: #cs_cluster_service_bind}

Crie credenciais de serviço de um serviço do {{site.data.keyword.cloud_notm}} e armazene essas credenciais em um segredo do Kubernetes em seu cluster. Para visualizar os serviços do {{site.data.keyword.cloud_notm}} disponíveis por meio do catálogo do {{site.data.keyword.cloud_notm}}, execute `ibmcloud service offerings`. **Nota**: é possível incluir apenas serviços do {{site.data.keyword.cloud_notm}} que suportam chaves de serviço.
{: shortdesc}

Para obter mais informações sobre a ligação de serviços e quais serviços podem ser incluídos em seu cluster, consulte [Incluindo serviços usando a ligação de serviços do IBM Cloud](/docs/containers?topic=containers-service-binding).



```
ibmcloud oc cluster-service-bind --cluster CLUSTER --namespace KUBERNETES_NAMESPACE --service SERVICE_INSTANCE [--key SERVICE_INSTANCE_KEY] [--role IAM_SERVICE_ROLE] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}} e a função **Desenvolvedor** do Cloud Foundry

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code> -- key  <em> SERVICE_INSTANCE_KEY </em> </code></dt>
<dd>O nome ou GUID de uma chave de serviço existente. Esse valor é opcional. Quando você usa o comando `service-binding`, as novas credenciais de serviço são criadas automaticamente para sua instância de serviço e designadas à função de acesso ao serviço **Gravador** do IAM para serviços ativados para IAM. Se desejar usar uma chave de serviço existente que você criou anteriormente, use essa opção. Se você definir uma chave de serviço, não será possível configurar a opção `--role` ao mesmo tempo porque suas chaves de serviço já estão criadas com uma função de acesso ao serviço IAM específica. </dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>O nome do namespace do Kubernetes no qual você deseja criar o segredo do Kubernetes para suas credenciais de serviço. Este valor é obrigatório.</dd>

<dt><code>--service <em>SERVICE_INSTANCE</em></code></dt>
<dd>O nome da instância de serviço do {{site.data.keyword.cloud_notm}} que você deseja ligar. Para localizar o nome, execute <code>ibmcloud service list</code> para os serviços do Cloud Foundry e <code>ibmcloud resource service-instances</code> para serviços ativados para IAM. Este valor é obrigatório. </dd>

<dt><code>--role <em>IAM_SERVICE_ROLE</em></code></dt>
<dd>A função do {{site.data.keyword.cloud_notm}} IAM que você deseja que a chave de serviço tenha. Esse valor é opcional e pode ser usado somente para serviços ativados para IAM. Se você não configurar essa opção, suas credenciais de serviço serão criadas automaticamente e designadas à função de acesso ao serviço **Gravador** do IAM. Se você desejar usar chaves de serviço existentes especificando a opção `--key`, não inclua essa opção.<br><br>
Para listar as funções disponíveis para o serviço, execute `ibmcloud iam roles --service <service_name>`. O nome do serviço é o nome do serviço no catálogo, que você pode obter executando `ibmcloud catalog search`.  </dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-service-bind --cluster my_cluster --namespace my_namespace --service my_service_instance
```
{: pre}

</br>
### `ibmcloud oc cluster-service-unbind`
{: #cs_cluster_service_unbind}

Remova um serviço do {{site.data.keyword.cloud_notm}} de um cluster, desvinculando-o de um namespace do Kubernetes.
{: shortdesc}



Quando você remove um serviço do {{site.data.keyword.cloud_notm}}, as credenciais de serviço são removidas do cluster. Se um pod ainda está usando o serviço,
ele falha porque as credenciais de serviço não podem ser localizadas.
{: tip}

```
ibmcloud oc cluster-service-unbind --cluster CLUSTER --namespace KUBERNETES_NAMESPACE --service SERVICE_INSTANCE [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}} e a função **Desenvolvedor** do Cloud Foundry

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>O nome do namespace do Kubernetes. Este valor é obrigatório.</dd>

<dt><code>--service <em>SERVICE_INSTANCE</em></code></dt>
<dd>O nome da instância de serviço do {{site.data.keyword.cloud_notm}} que você deseja remover. Para localizar o nome da instância de serviço, execute `ibmcloud oc cluster-services --cluster <cluster_name_or_ID>`. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-service-unbind --cluster my_cluster --namespace my_namespace --service 8567221
```
{: pre}

</br>
### `ibmcloud oc cluster-services`
{: #cs_cluster_services}

Listar os serviços que estão ligados a um ou todos os namespaces do Kubernetes em um cluster. Se nenhuma
opção é especificada, os serviços para o namespace padrão são exibidos.
{: shortdesc}



```
ibmcloud oc cluster-services --cluster CLUSTER [--namespace KUBERNETES_NAMESPACE] [--all-namespaces] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code>, <code>-n <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>Inclua os serviços que forem limitados a um namespace específico em um cluster. Esse valor é opcional.</dd>

<dt><code>--all-namespaces</code></dt>
<dd>Inclua os serviços que forem limitados a todos os namespaces em um cluster. Esse valor é opcional.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-services --cluster my_cluster --namespace my_namespace
```
{: pre}

</br>
### `ibmcloud oc va`
{: #cs_va}

Após você [instalar o scanner de contêiner](/docs/services/va?topic=va-va_index#va_install_container_scanner), visualize um relatório de avaliação de vulnerabilidade detalhado para um contêiner em seu cluster.
{: shortdesc}



```
ibmcloud oc va --container CONTAINER_ID [--extended] [--vulnerabilities] [--configuration-issues] [--json]
```
{: pre}

**Permissões mínimas necessárias**: função de acesso ao serviço **Leitor** para o {{site.data.keyword.registrylong_notm}}. **Nota**: não designe políticas ao {{site.data.keyword.registryshort_notm}} no nível do grupo de recursos.

**Opções de comando**:
<dl>
<dt><code>--container CONTAINER_ID</code></dt>
<dd><p>O ID do contêiner. Este valor é obrigatório.</p>
<p>Para localizar o ID de seu contêiner:<ol><li>[Direcione a CLI do Kubernetes para o seu cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).</li><li>Liste seus pods executando `oc get pods`.</li><li>Localize o campo **ID do contêiner** na saída do comando `oc describe pod <pod_name>`. Por exemplo,  ` Container ID: containerd://1a11a1aa2b2b22223333c44444ccc555667d7dd777888e8ef99f1011121314g15 `.</li><li>Remova o prefixo `containerd://` do ID antes de usar o ID do contêiner para o comando `ibmcloud oc va`. Por exemplo, `1a11a1aa2b2b22223333c44444ccc555667d7dd777888e8ef99f1011121314g15`.</li></ol></p></dd>

<dt><code>--extended</code></dt>
<dd><p>Estenda a saída de comando para mostrar mais informações de correção para pacotes vulneráveis. Esse valor é opcional.</p>
<p>Por padrão, os resultados da varredura mostram o ID, o status da política, os pacotes afetados e o modo de resolver. Com a sinalização `--extended`, isso inclui informações como o resumo, o aviso de segurança do fornecedor e o link de aviso oficial.</p></dd>

<dt><code>--vulnerabilities</code></dt>
<dd>Restrinja a saída de comando para mostrar apenas as vulnerabilidades do pacote. Esse valor é opcional. Não será possível usar essa sinalização se você usar a sinalização `--configuration-issues`.</dd>

<dt><code>--configuration-issues</code></dt>
<dd>Restrinja a saída de comando para mostrar apenas os problemas de configuração. Esse valor é opcional. Não será possível usar essa sinalização se você usar a sinalização `--vulnerabilities`.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc va --container 1a11a1aa2b2b22223333c44444ccc555667d7dd777888e8ef99f1011121314g15 --extended --vulnerabilities --json
```
{: pre}

</br>
### Beta: `ibmcloud oc key-protect-enable`
{: #cs_key_protect}

Criptografe seus segredos do Kubernetes usando o [{{site.data.keyword.keymanagementservicefull}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/key-protect?topic=key-protect-getting-started-tutorial#getting-started-tutorial) como um [provedor de serviço de gerenciamento de chaves (KMS) ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) em seu cluster. Para girar uma chave em um cluster com a criptografia de chave existente, execute novamente esse comando com um novo ID de chave raiz.
{: shortdesc}

Não exclua chaves raiz em sua instância do {{site.data.keyword.keymanagementserviceshort}}. Não exclua chaves mesmo se você girar para usar uma nova chave. Não será possível acessar ou remover os dados em etcd ou os dados dos segredos em seu cluster se você excluir uma chave raiz.
{: important}



```
ibmcloud oc key-protect-enable --cluster CLUSTER_NAME_OR_ID --key-protect-url ENDPOINT --key-protect-instance INSTANCE_GUID --crk ROOT_KEY_ID
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code> -- container CLUSTER_NAME_OR_ID </code></dt>
<dd>O nome ou ID do cluster.</dd>

<dt><code>--key-protect-url ENDPOINT </code></dt>
<dd>O terminal do  {{site.data.keyword.keymanagementserviceshort}}  para a instância do cluster. Para obter o terminal, veja [terminais em serviço por região](/docs/services/key-protect?topic=key-protect-regions#service-endpoints).</dd>

<dt><code>--key-protect-instance INSTANCE_GUID </code></dt>
<dd>Seu GUID da instância do  {{site.data.keyword.keymanagementserviceshort}} . Para obter o GUID da instância, execute <code>ibmcloud resource service-instance SERVICE_INSTANCE_NAME --id</code> e copie o segundo valor (não o CRN integral).</dd>

<dt><code> -- crk ROOT_KEY_ID </code></dt>
<dd>Seu ID da chave raiz  {{site.data.keyword.keymanagementserviceshort}} . Para obter o CRK, veja [Visualizando chaves](/docs/services/key-protect?topic=key-protect-view-keys#view-keys).</dd>
</dl>

**Exemplo**:
```
ibmcloud oc key-protect-enable --cluster mycluster --key-protect-url keyprotect.us-south.bluemix.net --key-protect-instance a11aa11a-bbb2-3333-d444-e5e555e5ee5 --crk 1a111a1a-bb22-3c3c-4d44-55e555e55e55
```
{: pre}

</br>
### `ibmcloud oc webhook-create`
{: #cs_webhook_create}

Registre um webhook.
{: shortdesc}



```
ibmcloud oc webhook-create --cluster CLUSTER --level LEVEL --type slack --url URL  [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--level <em>LEVEL</em></code></dt>
<dd>O nível de notificação, como <code>Normal</code> ou <code>Warning</code>. <code>Warning</code> é o valor padrão. Esse valor é opcional.</dd>

<dt><code>--type <em>slack</em></code></dt>
<dd>O tipo de webhook. Atualmente, o Slack é suportado. Este valor é obrigatório.</dd>

<dt><code>--url <em>URL</em></code></dt>
<dd>A URL para o webhook. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc webhook-create --cluster my_cluster --level Normal --type slack --url http://github.com/mywebhook
```
{: pre}

<br />


## Comandos do cluster: Subnets
{: #cluster_subnets_commands}



### `ibmcloud oc cluster-subnet-add`
{: #cs_cluster_subnet_add}

Disponibilize uma sub-rede pública ou privada móvel existente em sua conta de infraestrutura do IBM Cloud para um cluster ou reutilize sub-redes de um cluster excluído em vez de usar as sub-redes automaticamente provisionadas.
{: shortdesc}



<p class="important">Os endereços IP públicos móveis são cobrados mensalmente. Se você remover endereços IP públicos móveis após o provisionamento de seu cluster, ainda será necessário pagar o encargo mensal, mesmo que os tenha usado apenas por um curto período de tempo.</br>
</br>Ao disponibilizar uma sub-rede para um cluster, os endereços IP dessa sub-rede serão usados para propósitos de rede do cluster. Para evitar conflitos de endereço IP, certifique-se de usar uma sub-rede com somente um cluster. Não use uma sub-rede para diversos clusters ou para outros propósitos fora do {{site.data.keyword.containerlong_notm}} ao mesmo tempo.</br>
</br>Para ativar a comunicação entre trabalhadores que estão em sub-redes diferentes na mesma VLAN em contas não VRF, deve-se [ativar o roteamento entre sub-redes na mesma VLAN](/docs/containers?topic=containers-subnets#subnet-routing).</p>

```
ibmcloud oc cluster-subnet-add --cluster CLUSTER --subnet-id SUBNET [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code> -- subnet-id  <em> SUBNET </em> </code></dt>
<dd>O ID da sub-rede. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-subnet-add --cluster my_cluster --subnet-id 1643389
```
{: pre}

</br>

### `ibmcloud oc cluster-subnet-create`
{: #cs_cluster_subnet_create}

Crie uma sub-rede móvel em uma conta de infraestrutura do IBM Cloud em sua VLAN pública ou privada e torne-a disponível para um cluster.
{: shortdesc}



<p class="important">Quando você torna uma sub-rede disponível para um cluster, os endereços IP
dessa sub-rede são usados para propósitos de rede do cluster. Para evitar conflitos de endereço IP, certifique-se de usar uma sub-rede com somente um cluster. Não use uma sub-rede para diversos clusters ou para outros propósitos fora do {{site.data.keyword.containerlong_notm}} ao mesmo tempo.</br>
</br>Se você tiver múltiplas VLANs para um cluster, múltiplas sub-redes na mesma VLAN ou em um cluster multizona, você deverá ativar um [Virtual Router Function (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) para sua conta de infraestrutura do IBM Cloud para que os nós do trabalhador possam se comunicar entre si na rede privada. Para ativar o VRF, [entre em contato com o seu representante de conta de infraestrutura do IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Para verificar se um VRF já está ativado, use o comando `ibmcloud account show`. Se não for possível ou você não desejar ativar o VRF, ative o [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Para executar essa ação, você precisa da [permissão de infraestrutura](/docs/containers?topic=containers-users#infra_access) **Rede > Gerenciar a rede VLAN Spanning** ou é possível solicitar ao proprietário da conta para ativá-la. Para verificar se a ampliação da VLAN já está ativada, use o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud oc vlan-spanning-get --region <region>`.</p>

```
ibmcloud oc cluster-subnet-create --cluster CLUSTER --size SIZE --vlan VLAN_ID [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório. Para listar seus clusters, use o [comando](#cs_clusters) `ibmcloud oc clusters`.</dd>

<dt><code> -- size  <em> SIZE </em> </code></dt>
<dd>O número de endereços IP que você deseja criar na sub-rede móvel. Os valores aceitos são 8, 16, 32 ou 64. <p class="note"> Quando você inclui endereços IP móveis para sua sub-rede, três endereços IP são usados para estabelecer a rede interna do cluster. Não é possível usar esses três endereços IP para seus balanceadores de carga do aplicativo (ALBs) Ingress ou para criar serviços de balanceador de carga de rede (NLB). Por exemplo, se você solicitar oito endereços IP públicos móveis, será possível usar cinco deles para expor os seus apps ao público.</p> </dd>

<dt><code>--vlan <em>VLAN_ID</em></code></dt>
<dd>O ID da VLAN pública ou privada na qual você deseja criar a sub-rede. Deve-se selecionar uma VLAN pública ou privada à qual um nó do trabalhador existente está conectado. Para revisar as VLANs públicas ou privadas às quais seus nós do trabalhador estão conectados, execute <code>ibmcloud oc cluster-get --cluster &lt;cluster&gt; --showResources</code> e procure pela seção <strong>VLANs de sub-rede</strong> na saída. A sub-rede é provisionada na mesma zona em que a VLAN está.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-subnet-create --cluster my_cluster --size 8 --vlan 1764905
```
{: pre}

</br>

### `ibmcloud oc cluster-subnet-detach`
{: #cs_cluster_subnet_detach}

Remova uma sub-rede móvel pública ou privada em uma conta de infraestrutura do IBM Cloud de um cluster. A sub-rede permanece disponível em sua conta de infraestrutura do IBM Cloud. **Nota**: qualquer serviço que foi implementado em um endereço IP da sub-rede permanece ativo após a sub-rede ser removida.
{: shortdesc}

<p class="note"><img src="images/icon-classic.png" alt="Ícone de provedor de infraestrutura clássica" width="15" style="width:15px; border-style: none"/> Comando clássico apenas.</p>

```
ibmcloud oc cluster-subnet-detach --cluster CLUSTER --subent-id SUBNET_ID [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório. Para listar seus clusters, use o [comando](#cs_clusters) `ibmcloud oc clusters`.</dd>

<dt><code>--vlan <em>VLAN_ID</em></code></dt>
<dd>O ID da sub-rede pública ou privada que você deseja remover. Para localizar o ID de sub-rede, primeiro, execute <code>ibmcloud oc cluster-get --cluster &lt;cluster&gt; --showResources</code> e procure pelo CIDR de sub-rede na seção <strong>VLANs de sub-rede</strong> da saída. Em seguida, usando o CIDR da sub-rede, execute <code>ibmcloud oc subnets</code> e procure pelo <strong>ID</strong> da sub-rede.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-subnet-detach --cluster my_cluster --subnet-id 1602829
```
{: pre}

</br>

### `ibmcloud oc cluster-user-subnet-add`
{: #cs_cluster_user_subnet_add}

Traga a sua própria sub-rede privada para os seus clusters do {{site.data.keyword.containerlong_notm}}.
{: shortdesc}



Essa sub-rede privada não é fornecida pela infraestrutura do IBM Cloud. Como tal, deve-se configurar qualquer roteamento de tráfego de rede de entrada e saída para a sub-rede. Para incluir uma sub-rede de infraestrutura do IBM Cloud, use o [comando](#cs_cluster_subnet_add) `ibmcloud oc cluster-subnet-add`.

<p class="important">Quando você torna uma sub-rede disponível para um cluster, os endereços IP
dessa sub-rede são usados para propósitos de rede do cluster. Para evitar conflitos de endereço IP, certifique-se de usar uma sub-rede com somente um cluster. Não use uma sub-rede para diversos clusters ou para outros propósitos fora do {{site.data.keyword.containerlong_notm}} ao mesmo tempo.</br>
</br>Se você tiver múltiplas VLANs para um cluster, múltiplas sub-redes na mesma VLAN ou em um cluster multizona, você deverá ativar um [Virtual Router Function (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) para sua conta de infraestrutura do IBM Cloud para que os nós do trabalhador possam se comunicar entre si na rede privada. Para ativar o VRF, [entre em contato com o seu representante de conta de infraestrutura do IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Para verificar se um VRF já está ativado, use o comando `ibmcloud account show`. Se não for possível ou você não desejar ativar o VRF, ative o [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Para executar essa ação, você precisa da [permissão de infraestrutura](/docs/containers?topic=containers-users#infra_access) **Rede > Gerenciar a rede VLAN Spanning** ou é possível solicitar ao proprietário da conta para ativá-la. Para verificar se a ampliação da VLAN já está ativada, use o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud oc vlan-spanning-get --region <region>`.</p>

```
ibmcloud oc cluster-user-subnet-add --cluster CLUSTER --subnet-cidr SUBNET_CIDR --private-vlan PRIVATE_VLAN
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--subnet-cidr <em>SUBNET_CIDR</em></code></dt>
<dd>O Classless InterDomain Routing (CIDR) de sub-rede. Esse valor é necessário e não deve entrar em conflito com nenhuma sub-rede que é usada pela infraestrutura do IBM Cloud. Os prefixos suportados variam de `/30` (1 endereço IP) a `/24` (253 endereços IP). Se você definir o CIDR com um comprimento de prefixo e posteriormente precisar mudá-lo, primeiro inclua o novo CIDR, então, [remova o CIDR antigo](#cs_cluster_user_subnet_rm).</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>O ID da VLAN privada. Este valor é obrigatório. O ID deve ser para uma VLAN privada no cluster em que estão um ou mais nós do trabalhador. Para ver VLANs privadas em seu cluster, execute `ibmcloud oc cluster-get --cluster <cluster_name_or_ID> --showResources`. Na seção **VLANs de sub-rede** da saída, procure por VLANs que possuem um valor para **Público** de `false`.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-user-subnet-add --cluster my_cluster --subnet-cidr 169.xx.xxx.xxx/29 --private-vlan 1502175
```
{: pre}

</br>
### `ibmcloud oc cluster-user-subnet-rm`
{: #cs_cluster_user_subnet_rm}

Remova a sua própria sub-rede privada de um cluster especificado. Qualquer serviço que foi implementado com um endereço IP de sua própria sub-rede privada permanece ativo depois que a sub-rede é removida.
{: shortdesc}



```
ibmcloud oc cluster-user-subnet-rm --cluster CLUSTER --subnet-cidr SUBNET_CIDR --private-vlan PRIVATE_VLAN
```
{: pre}
**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--subnet-cidr <em>SUBNET_CIDR</em></code></dt>
<dd>O Classless InterDomain Routing (CIDR) de sub-rede. Esse valor é necessário e deve corresponder ao CIDR que foi configurado pelo [comando](#cs_cluster_user_subnet_add) `ibmcloud oc cluster-user-subnet-add`.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>O ID da VLAN privada. Esse valor é necessário e deve corresponder ao ID da VLAN que foi configurado pelo [comando](#cs_cluster_user_subnet_add) `ibmcloud oc cluster-user-subnet-add`.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc cluster-user-subnet-rm --cluster my_cluster --subnet-cidr 169.xx.xxx.xxx/29 --private-vlan 1502175
```
{: pre}

</br>
### `ibmcloud oc subnets`
{: #cs_subnets}

Liste as sub-redes móveis disponíveis em sua conta de infraestrutura do IBM Cloud.
{: shortdesc}



```
ibmcloud oc subnets [--locations LOCATIONS] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>

<dt><code>--locations <em>LOCATION</em></code></dt>
<dd>Filtre zonas por um local específico ou uma lista de locais separados por vírgula. Para ver as localizações suportadas, execute <code>ibmcloud oc supported-locations</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc subnets --locations ams03,wdc,ap
```
{: pre}

<br />


## Comandos do balanceador de carga do aplicativo (ALB) Ingress
{: #alb_commands}

### `ibmcloud oc alb-autoupdate-disable`
{: #cs_alb_autoupdate_disable}

Desative as atualizações automáticas de todos os pods do ALB do Ingress em um cluster.
{: shortdesc}



Por padrão, as atualizações automáticas para o complemento do balanceador de carga de aplicativo (ALB) do Ingress são ativadas. Os pods do ALB são atualizados automaticamente quando uma nova versão de construção está disponível. Atualize o complemento manualmente; use esse comando para desativar as atualizações automáticas. Em seguida, é possível atualizar os pods do ALB executando o [comando `ibmcloud oc alb-update`](#cs_alb_update).

Quando você atualiza a versão principal ou secundária do Kubernetes de seu cluster, a IBM faz as mudanças necessárias automaticamente na implementação do Ingress, mas não muda a versão de construção de seu complemento ALB do Ingress. Você é responsável por verificar a compatibilidade das versões mais recentes do Kubernetes e de suas imagens do complemento ALB do Ingress.

```
ibmcloud oc alb-autoupdate-disable --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Exemplo**:
```
ibmcloud oc alb-autoupdate-disable --cluster mycluster
```
{: pre}

</br>
### `ibmcloud oc alb-autoupdate-enable`
{: #cs_alb_autoupdate_enable}

Ative as atualizações automáticas de todos os pods do ALB do Ingress em um cluster.
{: shortdesc}

Se as atualizações automáticas para o complemento ALB de Ingress estiverem desativadas, será possível reativar as atualizações automáticas. Sempre que a próxima versão de construção se torna disponível, os ALBs são atualizados automaticamente para a construção mais recente.



```
ibmcloud oc alb-autoupdate-enable --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

</br>
### `ibmcloud oc alb-autoupdate-get`
{: #cs_alb_autoupdate_get}

Verifique se as atualizações automáticas para o complemento ALB do Ingress estão ativadas e se os ALBs são atualizados para a versão de construção mais recente.
{: shortdesc}



```
ibmcloud oc alb-autoupdate-get --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

</br>
### Beta: `ibmcloud oc alb-cert-deploy`
{: #cs_alb_cert_deploy}

Implemente ou atualize um certificado de sua instância do {{site.data.keyword.cloudcerts_long_notm}} para o ALB em um cluster.
{: shortdesc}



Quando você importa um certificado com esse comando, o segredo do certificado é criado em um namespace chamado `ibm-cert-store`. Uma referência a esse segredo é, então, criada no namespace `default`, que qualquer recurso Ingress em qualquer namespace pode acessar. Quando o ALB está processando solicitações, ele segue essa referência para selecionar e usar o segredo do certificado por meio do namespace `ibm-cert-store`.

Também é possível usar o parâmetro `--update` para atualizar certificados, como atualizar o certificado em seu cluster depois de renovar o certificado no {{site.data.keyword.cloudcerts_short}}. É possível atualizar os certificados que são importados da mesma instância do {{site.data.keyword.cloudcerts_long_notm}} apenas.

Para permanecer dentro dos [limites de taxa](https://cloud.ibm.com/apidocs/certificate-manager#rate-limiting) configurados por {{site.data.keyword.cloudcerts_short}}, aguarde pelo menos 45 segundos entre os comandos `alb-cert-deploy` e `alb-cert-deploy -- update sucessivos`.
{: note}

```
ibmcloud oc alb-cert-deploy [--update] --cluster CLUSTER --secret-name SECRET_NAME --cert-crn CERTIFICATE_CRN [--update] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comandos**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--update</code></dt>
<dd>Atualize o certificado para um segredo do ALB em um cluster. É possível usar esse parâmetro para atualizar o certificado depois de renová-lo no {{site.data.keyword.cloudcerts_short}}.</dd>

<dt><code>--secret-name <em>SECRET_NAME</em></code></dt>
<dd>Especifique um nome para o segredo do ALB quando ele for criado no cluster. Este valor é obrigatório. Certifique-se de que você não crie o segredo com o mesmo nome que o segredo de Ingress fornecido pela IBM. É possível obter o nome do segredo do Ingress fornecido pela IBM executando <code>ibmcloud oc cluster-get --cluster <cluster_name_or_ID> | grep Ingress</code>.</dd>

<dt><code>--cert-crn <em>CERTIFICATE_CRN</em></code></dt>
<dd>O CRN do certificado. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplos**:

Exemplo para implementar um segredo do ALB:
```
ibmcloud oc alb-cert-deploy --secret-name my_alb_secret --cluster my_cluster --cert-crn crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:4bc35b7e0badb304e60aef00947ae7ff
```
{: pre}

Exemplo para atualizar um segredo do ALB existente:
```
ibmcloud oc alb-cert-deploy --update --secret-name my_alb_secret --cluster my_cluster --cert-crn crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:7e21fde8ee84a96d29240327daee3eb2
```
{: pre}

</br>
### Beta: `ibmcloud oc alb-cert-get`
{: #cs_alb_cert_get}

Se você importou um certificado do {{site.data.keyword.cloudcerts_short}} para o ALB em um cluster, visualize informações sobre o certificado TLS, como os segredos que estão associados a ele.
{: shortdesc}



```
ibmcloud oc alb-cert-get --cluster CLUSTER [--secret-name SECRET_NAME] [--cert-crn CERTIFICATE_CRN] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comandos**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--secret-name <em>SECRET_NAME</em></code></dt>
<dd>O nome do segredo do ALB. Esse valor é necessário para obter informações sobre um segredo do ALB específico no cluster.</dd>

<dt><code>--cert-crn <em>CERTIFICATE_CRN</em></code></dt>
<dd>O CRN do certificado. Esse valor é necessário para obter informações sobre todos os segredos do ALB que correspondem a um CRN de certificado específico no cluster.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplos**:

Exemplo para obter informações sobre um segredo do ALB:
```
ibmcloud oc alb-cert-get --cluster my_cluster --secret-name my_alb_secret
```
{: pre}

Exemplo para obter informações sobre todos os segredos do ALB que correspondem a um CRN de certificado especificado:
```
ibmcloud oc alb-cert-get --cluster my_cluster --cert-crn  crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:4bc35b7e0badb304e60aef00947ae7ff
```
{: pre}

</br>
### Beta: `ibmcloud oc alb-cert-rm`
{: #cs_alb_cert_rm}

Se você importou um certificado do {{site.data.keyword.cloudcerts_short}} para o ALB em um cluster, remova o segredo do cluster.
{: shortdesc}



Para permanecer dentro dos [limites de taxa](https://cloud.ibm.com/apidocs/certificate-manager#rate-limiting) configurados por {{site.data.keyword.cloudcerts_short}}, aguarde pelo menos 45 segundos entre os comandos `alb-cert-rm` sucessivos.
{: note}

```
ibmcloud oc alb-cert-rm --cluster CLUSTER [--secret-name SECRET_NAME] [--cert-crn CERTIFICATE_CRN] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comandos**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--secret-name <em>SECRET_NAME</em></code></dt>
<dd>O nome do segredo do ALB. Esse valor é necessário para remover um segredo do ALB específico no cluster.</dd>

<dt><code>--cert-crn <em>CERTIFICATE_CRN</em></code></dt>
<dd>O CRN do certificado. Esse valor é necessário para remover todos os segredos ALB que correspondem a um CRN de certificado específico no cluster.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>

</dl>

**Exemplos**:

Exemplo para remover um segredo do ALB:
```
ibmcloud oc alb-cert-rm --cluster my_cluster --secret-name my_alb_secret
```
{: pre}

Exemplo para remover todos os segredos do ALB que correspondem a um CRN de certificado especificado:
```
ibmcloud oc alb-cert-rm --cluster my_cluster --cert-crn crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:4bc35b7e0badb304e60aef00947ae7ff
```
{: pre}

</br>
### `ibmcloud oc alb-certs`
{: #cs_alb_certs}

Liste os certificados que você importou de sua instância do {{site.data.keyword.cloudcerts_long_notm}} para os ALBs em um cluster.
{: shortdesc}



```
ibmcloud oc alb-certs --cluster CLUSTER [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comandos**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc alb-certs --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc alb-configure`
{: #cs_alb_configure}

Ative ou desative um ALB em seu cluster padrão.
{: shortdesc}

É possível usar esse comando para:
* Ative um ALB privado padrão. Ao criar um cluster, um ALB privado padrão é criado em cada zona na qual você tem trabalhadores e em uma sub-rede privada disponível, mas os ALBs privados padrão não são ativados. No entanto, todos os ALBs públicos padrão são ativados automaticamente.
* Ative um ALB que você desativou anteriormente.
* Desative um ALB.
* Desative a implementação do ALB fornecido pela IBM para que seja possível implementar seu próprio controlador do Ingress e alavancar o registro DNS para o subdomínio do Ingress fornecido pela IBM ou o serviço de balanceador de carga usado para expor o controlador do Ingress.

```
ibmcloud oc alb-configure --albID ALB_ID --disable|--enable [--user-ip USER_IP]|--disable-deployment [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--albID <em>ALB_ID</em></code></dt>
<dd>O ID para um ALB. Para visualizar os IDs para os ALBs em um cluster, execute <code>ibmcloud oc albs --cluster <em>CLUSTER</em></code>. Este valor é obrigatório.</dd>

<dt><code>--disable</code></dt>
<dd>Inclua essa sinalização para desativar um ALB em um cluster. <p class="note">Se você desativar um ALB, o endereço IP usado pelo ALB voltará para o conjunto de IPs móveis disponíveis para que outro serviço possa usar o IP. Se depois você tentar reativar o ALB, o ALB poderá relatar um erro se o endereço IP que ele usou anteriormente estiver agora em uso por outro serviço. Será possível parar a execução do outro serviço ou especificar outro endereço IP a ser usado quando você reativar o ALB.</p></dd>

<dt><code>--enable</code></dt>
<dd>Inclua essa sinalização para ativar um ALB em um cluster.</dd>

<dt><code>--user-ip <em>USER_IP</em></code></dt>
<dd>Opcional: se você ativar o ALB com a sinalização <code>--enable</code>, será possível especificar um endereço IP que esteja em uma VLAN na zona em que o ALB foi criado. O ALB é ativado e usa esse endereço IP público ou privado. <strong>Nota</strong>: esse endereço IP não deve estar em uso por outro balanceador de carga ou ALB no cluster. Se nenhum endereço IP for fornecido, o ALB será implementado com um endereço IP público ou privado da sub-rede pública ou privada móvel que foi provisionada automaticamente quando você criou o cluster ou o endereço IP público ou privado designado anteriormente para o ALB.</dd>

<dt><code> --disable-deployment </code></dt>
<dd>Inclua essa sinalização para desativar a implementação do ALB fornecido pela IBM. Essa sinalização não remove o registro de DNS para o subdomínio do Ingress fornecido pela IBM ou o serviço de balanceador de carga que é usado para expor o controlador do Ingress.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplos**:

Exemplo para ativar um ALB:
```
ibmcloud oc alb-configure --albID private-cr18a61a63a6a94b658596aa93a087aaa9-alb1 --enable
```
{: pre}

Exemplo para ativar um ALB com um endereço IP fornecido pelo usuário:
```
ibmcloud oc alb-configure --albID private-cr18a61a63a6a94b658596aa93a087aaa9-alb1 --enable --user-ip user_ip
```
{: pre}

Exemplo para desativar um ALB:
```
ibmcloud oc alb-configure --albID public-cr18a61a63a6a94b658596aa93a087aaa9-alb1 --disable
```
{: pre}

</br>

### `ibmcloud oc alb-get`
{: #cs_alb_get}

Visualize os detalhes de um ALB do Ingress em um cluster.
{: shortdesc}



```
ibmcloud oc alb-get --albID ALB_ID [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--albID <em>ALB_ID</em></code></dt>
<dd>O ID para um ALB. Para visualizar os IDs para os ALBs em um cluster, execute <code>ibmcloud oc albs --cluster <em>CLUSTER</em></code>. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc alb-get --albID public-cr18a61a63a6a94b658596aa93a087aaa9-alb1
```
{: pre}

</br>
### `ibmcloud oc alb-rollback`
{: #cs_alb_rollback}

Se os pods do ALB foram atualizados recentemente, mas uma configuração customizada para seus ALBs foi afetada pela construção mais recente, será possível recuperar a atualização para a construção em que os pods do ALB estavam em execução anteriormente. Todos os pods do ALB em seu cluster revertem para o estado de execução anterior.
{: shortdesc}

Depois de retroceder uma atualização, as atualizações automáticas para os pods do ALB são desativadas. Para reativar as atualizações automáticas, use o [comando `alb-autoupdate-enable`](#cs_alb_autoupdate_enable).



```
ibmcloud oc alb-rollback --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

</br>
### `ibmcloud oc alb-types`
{: #cs_alb_types}

Listar tipos ALB do Ingress que são suportados.
{: shortdesc}



```
ibmcloud oc alb-types [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

</br>

### `ibmcloud oc alb-update`
{: #cs_alb_update}

Force uma atualização dos pods do ALB do Ingress no cluster para a versão mais recente.
{: shortdesc}



Se as atualizações automáticas para o complemento ALB do Ingress estiverem desativadas e você desejar atualizar o complemento, será possível forçar uma atualização única de seus pods do ALB. Quando você escolhe atualizar manualmente o complemento, todos os pods do ALB no cluster são atualizados para a construção mais recente. Não é possível atualizar um ALB individual ou escolher para qual construção atualizar o complemento. As atualizações automáticas permanecem desativadas.

Quando você atualiza a versão principal ou secundária do Kubernetes de seu cluster, a IBM faz as mudanças necessárias automaticamente na implementação do Ingress, mas não muda a versão de construção de seu complemento ALB do Ingress. Você é responsável por verificar a compatibilidade das versões mais recentes do Kubernetes e de suas imagens do complemento ALB do Ingress.

```
ibmcloud oc alb-update --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

</br>
### `ibmcloud oc albs`
{: #cs_albs}

Liste todos os IDs do ALB do Ingress em um cluster e visualize se uma atualização para os pods do ALB está disponível.
{: shortdesc}



Se nenhum ID de ALB for retornado, o cluster não terá uma sub-rede móvel. É possível [criar](#cs_cluster_subnet_create) ou [incluir](#cs_cluster_subnet_add) sub-redes em um cluster.
{: tip}

```
ibmcloud oc albs --cluster CLUSTER [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code><em>--cluster </em>CLUSTER</code></dt>
<dd>O nome ou ID do cluster no qual você lista os ALBs disponíveis. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc albs --cluster my_cluster
```
{: pre}

<br />



## Comandos de infraestrutura
{: #infrastructure_commands}

### `ibmcloud oc api-key-info`
{: #cs_api_key_info}

Visualize o nome e o endereço de e-mail para o proprietário da chave de API do {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) em um grupo de recursos do {{site.data.keyword.containerlong_notm}}.
{: shortdesc}



A chave de API do {{site.data.keyword.cloud_notm}} é configurada automaticamente para um grupo de recursos e região quando a primeira ação que requer a política de acesso de administrador do {{site.data.keyword.containerlong_notm}} é executada. Por exemplo, um de seus usuários administradores cria o primeiro cluster no grupo de recursos `default` na região `us-south`. Ao fazer isso, a chave de API do {{site.data.keyword.cloud_notm}} IAM para esse usuário é armazenada na conta para esse grupo de recursos e região. A chave de API é usada para pedir recursos na infraestrutura do IBM Cloud, como novos nós do trabalhador ou VLANs. Uma chave API diferente pode ser configurada para cada região dentro de um grupo de recursos.

Quando um usuário diferente executa uma ação nesse grupo de recursos e na região que requer interação com o portfólio de infraestrutura do IBM Cloud, como criar um novo cluster ou recarregar um nó do trabalhador, a chave de API armazenada é usada para determinar se existem permissões suficientes para executar essa ação. Para certificar-se de que as ações relacionadas à infraestrutura em seu cluster possam ser executadas com sucesso, designe a seus usuários administradores do {{site.data.keyword.containerlong_notm}} a política de acesso de infraestrutura **Superusuário**. Para obter mais informações, veja [Gerenciando o acesso de usuário](/docs/containers?topic=containers-users#infra_access).

Se você achar que precisa atualizar a chave de API armazenada para um grupo de recursos e uma região, será possível fazer isso executando o comando [ibmcloud oc api-key-reset](#cs_api_key_reset). Esse comando requer a política de acesso de administrador do {{site.data.keyword.containerlong_notm}} e armazena a chave API do usuário que executa esse comando na conta.

**Dica:** a chave de API que é retornada nesse comando pode não ser usada se as credenciais de infraestrutura do IBM Cloud foram configuradas manualmente usando o comando [ibmcloud oc credential-set](#cs_credentials_set).

```
ibmcloud oc api-key-info --cluster CLUSTER [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>

</dl>

**Exemplo**:
```
ibmcloud oc api-key-info --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc api-key-reset`
{: #cs_api_key_reset}

Substitua a chave de API do {{site.data.keyword.cloud_notm}} IAM atual em um grupo de recursos do {{site.data.keyword.cloud_notm}} e uma região do {{site.data.keyword.containershort_notm}}.
{: shortdesc}



Esse comando requer a política de acesso de administrador do {{site.data.keyword.containerlong_notm}} e armazena a chave API do usuário que executa esse comando na conta. A chave de API do {{site.data.keyword.cloud_notm}} IAM é necessária para pedir a infraestrutura do portfólio de infraestrutura do IBM Cloud. Quando armazenada, a chave API é usada para cada ação em uma região que requer permissões de infraestrutura independentemente do usuário que executa esse comando. Para obter mais informações sobre como as chaves de API do {{site.data.keyword.cloud_notm}} IAM funcionam, consulte o [comando `ibmcloud oc api-key-info`](#cs_api_key_info).

Antes de usar esse comando, certifique-se de que o usuário que executa esse comando tenha [o {{site.data.keyword.containerlong_notm}} e as permissões de infraestrutura do IBM Cloud](/docs/containers?topic=containers-users#users) necessárias. Tenha como destino o grupo de recursos e a região para os quais você deseja configurar a chave de API.
{: important}

```
ibmcloud oc api-key-reset --region REGION [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code> -- region  <em> REGION </em> </code></dt>
<dd>Especifique uma região. Para listar as regiões disponíveis, execute <code>ibmcloud oc regions</code>.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc api-key-reset --region us-south
```
{: pre}


</br>

### `ibmcloud oc credential-get`
{: #cs_credential_get}

Se você configurar a sua conta do {{site.data.keyword.cloud_notm}} para usar credenciais diferentes para acessar o portfólio de infraestrutura do IBM Cloud, obtenha o nome de usuário da infraestrutura para a região e o grupo de recursos de destino atualmente.
{: shortdesc}



```
ibmcloud oc credential-get --region REGION [-s] [--json]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code> -- region  <em> REGION </em> </code></dt>
<dd>Especifique uma região. Para listar as regiões disponíveis, execute <code>ibmcloud oc regions</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc credential-get --region us-south
```
{: pre}

</br>
### `ibmcloud oc credential-set` (`credentials-set`)
{: #cs_credentials_set}

Configure as credenciais para um grupo de recursos e uma região para que você possa acessar o portfólio de infraestrutura do IBM Cloud por meio de sua conta do {{site.data.keyword.cloud_notm}}.
{: shortdesc}



Se você tiver uma conta pré-paga do {{site.data.keyword.cloud_notm}}, você terá acesso ao portfólio de infraestrutura do IBM Cloud por padrão. No entanto, talvez você queira usar uma conta de infraestrutura do IBM Cloud diferente que você já tenha para pedir a infraestrutura. É possível vincular essa conta de infraestrutura à sua conta do {{site.data.keyword.cloud_notm}} conta usando este comando.

Se as credenciais de infraestrutura do IBM Cloud forem configuradas manualmente para uma região e um grupo de recursos, essas credenciais serão usadas para pedir a infraestrutura para todos os clusters nessa região no grupo de recursos. Essas credenciais são usadas para determinar permissões de infraestrutura, mesmo se uma [chave de API do {{site.data.keyword.cloud_notm}} IAM](#cs_api_key_info) existe para o grupo de recursos e a região. Se o usuário cujas credenciais estão armazenadas não tiver as permissões necessárias para pedir a infraestrutura, as ações relacionadas à infraestrutura, como a criação de um cluster ou o recarregamento de um nó do trabalhador, poderão falhar.

Não é possível configurar múltiplas credenciais para o mesmo grupo de recursos e região do {{site.data.keyword.containerlong_notm}}.

Antes de usar esse comando, certifique-se de que o usuário cujas credenciais são usadas tenha [o {{site.data.keyword.containerlong_notm}} e as permissões de infraestrutura do IBM Cloud](/docs/containers?topic=containers-users#users) necessárias.
{: important}

```
ibmcloud oc credential-set --infrastructure-api-key API_KEY --infrastructure-username USERNAME --region REGION [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--infrastructure-username <em>USERNAME</em></code></dt>
<dd>Nome de usuário da API da conta da infraestrutura do IBM Cloud. Este valor é obrigatório. O nome de usuário da API de infraestrutura não é o mesmo que o IBMid. Para visualizar o nome do usuário da API de infraestrutura, consulte [Gerenciando chaves de API de infraestrutura clássica](/docs/iam?topic=iam-classic_keys).</dd>

<dt><code>--infrastructure-api-key <em>API_KEY</em></code></dt>
<dd>Chave da API da conta da infraestrutura do IBM Cloud. Este valor é obrigatório. Para visualizar ou gerar uma chave de API de infraestrutura, consulte [Gerenciando chaves de API de infraestrutura clássica](/docs/iam?topic=iam-classic_keys).</dd>

<dt><code> -- region  <em> REGION </em> </code></dt>
<dd>Especifique uma região. Para listar as regiões disponíveis, execute <code>ibmcloud oc regions</code>.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc credential-set --infrastructure-api-key <api_key> --infrastructure-username dbmanager --region us-south
```
{: pre}

</br>
### `ibmcloud oc credential-unset`
{: #cs_credentials_unset}

Remova as credenciais para um grupo de recursos e região para remover o acesso ao portfólio de infraestrutura do IBM Cloud por meio de sua conta do {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Depois de remover as credenciais, a [chave de API do {{site.data.keyword.cloud_notm}} IAM](#cs_api_key_info) é usada para pedir recursos na infraestrutura do IBM Cloud.



```
ibmcloud oc credential-unset --region REGION [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code> -- region  <em> REGION </em> </code></dt>
<dd>Especifique uma região. Para listar as regiões disponíveis, execute <code>ibmcloud oc regions</code>.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc credential-unset --region us-south
```
{: pre}

</br>

### `ibmcloud oc flavors` (`machine-types`)
{: #cs_machine_types}

Visualize uma lista de tipos de nós do trabalhador disponíveis. Os tipos variam por zona.
{:shortdesc}



Cada tipo inclui a quantidade de CPU virtual, memória e espaço em disco para cada nó do trabalhador no cluster. Por padrão, o diretório do disco de armazenamento secundário em que todos os dados do contêiner são armazenados é criptografado com a criptografia LUKS. Se a opção `disable-disk-encrypt` for incluída durante a criação do cluster, os dados de tempo de execução do contêiner do host não serão criptografados. [ Saiba mais sobre a criptografia ](/docs/containers?topic=containers-security#encrypted_disk).

É possível provisionar o nó do trabalhador como uma máquina virtual no hardware compartilhado ou dedicado, ou para clusters clássicos apenas, como uma máquina física em bare metal. [Saiba mais sobre suas opções de tipo](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes).

```
ibmcloud oc flavors --zone ZONE [--json] [-s]
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

**Opções de comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Insira a zona na qual você deseja listar os tipos disponíveis. Este valor é obrigatório. Para ver as zonas disponíveis para clusters clássicos, execute `ibmcloud oc zones`.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc flavors --zone dal10
```
{: pre}


</br>

### `ibmcloud oc infra-permissions-get`
{: #infra_permissions_get}

Verifique se permissões de infraestrutura sugeridas ou necessárias estão ausentes das credenciais que permitem o [acesso ao portfólio de infraestrutura do IBM Cloud](/docs/containers?topic=containers-users#api_key) para o grupo de recursos e a região de destino.
{: shortdesc}



**O que as permissões de infraestrutura `required` e `suggested` significam?**<br>
Se as credenciais de infraestrutura para a região e o grupo de recursos estiverem omitindo quaisquer permissões, a saída desse comando retornará uma lista de permissões `required` e `suggested`.
*   **Necessário**: essas permissões são necessárias para pedir e gerenciar com êxito os recursos de infraestrutura, como nós do trabalhador. Se as credenciais de infraestrutura estiverem omitindo uma dessas permissões, as ações comuns, como `worker-reload`, poderão falhar para todos os clusters na região e no grupo de recursos.
*   **Sugerido**: essas permissões são úteis para incluir em suas permissões de infraestrutura e podem ser necessárias em determinados casos de uso. Por exemplo, a permissão de infraestrutura `Add Compute with Public Network Port` será sugerida porque, se você desejar rede pública, precisará dessa permissão. No entanto, se seu caso de uso for um cluster somente na VLAN privada, a permissão não será necessária, portanto, ela não será considerada `required`.

Para obter uma lista de casos de uso comuns por permissão, consulte [Funções de infraestrutura](/docs/containers?topic=containers-access_reference#infra).

**E se eu vir uma permissão de infraestrutura que não posso localizar no console ou na tabela [Funções de infraestrutura](/docs/containers?topic=containers-access_reference#infra)?**<br>
As permissões de `Support Case` são gerenciadas em uma parte diferente do console do que as permissões de infraestrutura. Consulte a etapa 8 de [Customizando permissões de infraestrutura](/docs/containers?topic=containers-users#infra_access).

**Quais permissões de infraestrutura designar?**<br>
Se as políticas da sua empresa para permissões forem restritas, você poderá precisar limitar as permissões `suggested` para o caso de uso do seu cluster. Caso contrário, certifique-se de que suas credenciais de infraestrutura para a região e o grupo de recursos incluam todas as permissões `required` e `suggested`.

Para a maioria dos casos de uso, [configure a chave de API](/docs/containers?topic=containers-users#api_key) para a região e o grupo de recursos com as permissões de infraestrutura apropriadas. Se for necessário usar outra conta de infraestrutura que seja diferente de sua conta atual, [configure credenciais manuais](/docs/containers?topic=containers-users#credentials).

**Como controlar quais ações os usuários podem executar?**<br>
Após as credenciais de infraestrutura serem configuradas, é possível controlar quais ações seus usuários podem executar designando a eles [funções da plataforma do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-access_reference#iam_platform).

```
ibmcloud oc infra-permissions-get --region REGION [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code> -- region  <em> REGION </em> </code></dt>
<dd>Especifique uma região. Para listar as regiões disponíveis, execute <code>ibmcloud oc regions</code>. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc infra-permissions-get --region us-south
```
{: pre}

Saída de exemplo:
```
Missing Virtual Worker Permissions

Add Server                    suggested
Cancel Server                 suggested
View Virtual Server Details   required

Missing Physical Worker Permissions

Nenhuma mudança é sugerida ou necessária.

Missing Network Permissions

Nenhuma mudança é sugerida ou necessária.

Missing Storage Permissions

Add Storage       required
Manage Storage    required
```
{: screen}


</br>

### `ibmcloud oc vlan-spanning-get`
{: #cs_vlan_spanning_get}

Visualize o status da ampliação de VLAN para uma conta de infraestrutura do IBM Cloud. A ampliação de VLAN permite que todos os dispositivos em uma conta se comuniquem entre si por meio da rede privada, independentemente de sua VLAN designada.
{: shortdesc}

<p class="note">A opção Ampliação de VLAN é desativada para clusters que são criados em uma conta ativada por VRF. Quando o VRF é ativado, todas as VLANs na conta podem se comunicar automaticamente entre si por meio da rede privada. Para verificar se um VRF está ativado, use o comando `ibmcloud account show`. Para obter mais informações, consulte [Planejando a configuração de rede do cluster: comunicação de trabalhador para trabalhador](/docs/containers?topic=containers-plan_clusters#worker-worker).</p>

```
ibmcloud oc vlan-spanning-get --region REGION [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code> -- region  <em> REGION </em> </code></dt>
<dd>Especifique uma região. Para listar as regiões disponíveis, execute <code>ibmcloud oc regions</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc vlan-spanning-get --region us-south
```
{: pre}

</br>
### `ibmcloud oc vlans`
{: #cs_vlans}

Liste as VLANs públicas e privadas que estão disponíveis para uma zona em sua conta de infraestrutura do IBM Cloud. Para listar as VLANs disponíveis, deve-se
ter uma conta paga.
{: shortdesc}



```
ibmcloud oc vlans --zone ZONE [--all] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**:
* Para visualizar as VLANs às quais o cluster está conectado em uma zona: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}
* Para listar todas as VLANs disponíveis em uma zona: a função da plataforma **Visualizador** para a região no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Insira a zona na qual você deseja listar as suas VLANs privadas e públicas. Este valor é obrigatório. Para ver as zonas disponíveis, execute `ibmcloud oc zones`.</dd>

<dt><code>--all</code></dt>
<dd>Lista todas as VLANs disponíveis. Por padrão, as VLANs são filtradas para mostrar apenas as VLANs que são válidas. Para ser válida, uma VLAN deve ser associada à infraestrutura que pode hospedar um trabalhador com armazenamento em disco local.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc vlans --zone dal10
```
{: pre}

</br>


<br />


## Comandos de criação de log
{: #logging_commands}

### `ibmcloud oc apiserver-config-get audit-webhook`
{: #cs_apiserver_config_get}

Visualize a URL para o serviço de criação de log remoto para o qual você está enviando logs de auditoria do servidor de API. A URL foi especificada quando você criou o back-end do webhook para a configuração do servidor de API.
{: shortdesc}



```
ibmcloud oc apiserver-config-get audit-webhook --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>
</dl>

</br>

### `ibmcloud oc apiserver-config-set audit-webhook`
{: #cs_apiserver_config_set}

Configure o backend do webhook para a configuração do servidor de API. O back-end do webhook encaminha os logs de auditoria do servidor de API para um servidor remoto. Uma configuração de webhook é criada com base nas informações fornecidas nas sinalizações desse comando. Se você não fornecer nenhuma informação nas sinalizações, uma configuração de webhook padrão será usada. Após configurar o webhook, deve-se executar o comando `ibmcloud oc apiserver-refresh` para aplicar as mudanças no mestre do Kubernetes.
{: shortdesc}



```
ibmcloud oc apiserver-config-set audit-webhook --cluster CLUSTER [--remoteServer SERVER_URL_OR_IP] [--caCert CA_CERT_PATH] [--clientCert CLIENT_CERT_PATH] [--clientKey CLIENT_KEY_PATH]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--remoteServer <em>SERVER_URL</em></code></dt>
<dd>A URL ou o endereço IP para o serviço de criação de log remoto para o qual deseja enviar logs de auditoria. Se você fornecer uma URL insegura do servidor, todos os certificados serão ignorados. Esse valor é opcional.</dd>

<dt><code>--caCert <em>CA_CERT_PATH</em></code></dt>
<dd>O caminho de arquivo para o certificado de CA que é usado para verificar o serviço de criação de log remoto. Esse valor é opcional.</dd>

<dt><code>--clientCert <em>CLIENT_CERT_PATH</em></code></dt>
<dd>O caminho de arquivo para o certificado de cliente que é usado para autenticar com relação ao serviço de criação de log remoto. Esse valor é opcional.</dd>

<dt><code>--clientKey <em> CLIENT_KEY_PATH</em></code></dt>
<dd>O caminho de arquivo para a chave do cliente correspondente que é usada para se conectar ao serviço de criação de log remoto. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc apiserver-config-set audit-webhook --cluster my_cluster --remoteServer https://audit.example.com/audit --caCert /mnt/etc/kubernetes/apiserver audit/ca.pem --clientCert /mnt/etc/kubernetes/apiserver audit/cert.pem --clientKey /mnt/etc/kubernetes/apiserver audit/key.pem
```
{: pre}

</br>
### `ibmcloud oc apiserver-config-unset audit-webhook`
{: #cs_apiserver_config_unset}

Desative a configuração de backend de webhook para o servidor de API do cluster. Desativando o back-end do webhook para o encaminhamento de logs de auditoria do servidor de API para um servidor remoto.
{: shortdesc}



```
ibmcloud oc apiserver-config-unset audit-webhook --cluster CLUSTER
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>
</dl>

</br>

### `ibmcloud oc logging-autoupdate-disable`
{: #cs_log_autoupdate_disable}

Desative atualizações automáticas de todos os pods do Fluentd em um cluster.
{: shortdesc}



Desative as atualizações automáticas de seus pods do Fluentd em um cluster específico. Quando você atualiza a versão principal ou secundária do Kubernetes de seu cluster, a IBM automaticamente faz mudanças necessárias no Fluentd configmap, mas não muda a versão de construção de seu Fluentd para criação de log de complemento. Você é responsável por verificar a compatibilidade das versões mais recentes do Kubernetes e de suas imagens de complementos.

```
ibmcloud oc logging-autoupdate-disable --cluster CLUSTER
```
{: pre}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou o ID do cluster no qual você deseja desativar as atualizações automáticas para o complemento Fluentd. Este valor é obrigatório.</dd>
</dl>

</br>

### `ibmcloud oc logging-autoupdate-enable`
{: #cs_log_autoupdate_enable}

Ative atualizações automáticas para seus pods Fluentd em um cluster específico. Os pods do Fluentd são atualizados automaticamente quando uma nova versão de construção está disponível.
{: shortdesc}



```
ibmcloud oc logging-autoupdate-enable --cluster CLUSTER
```
{: pre}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou o ID do cluster no qual você deseja ativar atualizações automáticas para o complemento Fluentd. Este valor é obrigatório.</dd>
</dl>

</br>

### `ibmcloud oc logging-autoupdate-get`
{: #cs_log_autoupdate_get}

Visualize se seus pods do Fluentd estão configurados para serem atualizados automaticamente em um cluster.
{: shortdesc}



```
ibmcloud oc logging-autoupdate-get --cluster CLUSTER
```
{: pre}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster em que você deseja verificar se as atualizações automáticas para o complemento Fluentd estão ativadas. Este valor é obrigatório.</dd>
</dl>

</br>

### `ibmcloud oc logging-collect`
{: #cs_log_collect}

Faça uma solicitação para obter uma captura instantânea de seus logs em um momento específico e, em seguida, armazene os logs em um depósito do {{site.data.keyword.cos_full_notm}}.
{: shortdesc}



```
ibmcloud oc logging-collect --cluster CLUSTER --cos-bucket BUCKET_NAME --cos-endpoint ENDPOINT --hmac-key-id HMAC_KEY_ID --hmac-key HMAC_KEY --type LOG_TYPE [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster para o qual você deseja criar uma captura instantânea.</dd>

<dt><code>--cos-bucket <em>BUCKET_NAME</em></code></dt>
<dd>O nome do bucket do {{site.data.keyword.cos_short}} no qual você deseja armazenar os logs.</dd>

<dt><code> -- cos-endpoint  <em> ENDPOINT </em> </code></dt>
<dd>O terminal do data center regional, entre regionais ou único do {{site.data.keyword.cos_short}} do depósito no qual você está armazenando seus logs. Para obter os terminais disponíveis, consulte [Terminais e locais de armazenamento](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints) na documentação do {{site.data.keyword.cos_short}}.</dd>

<dt><code>--hmac-key-id  <em> HMAC_KEY_ID </em> </code></dt>
<dd>O ID exclusivo para suas credenciais HMAC de sua instância do {{site.data.keyword.cos_short}}.</dd>

<dt><code> -- hmac-key  <em> HMAC_KEY </em> </code></dt>
<dd>A chave HMAC para sua instância do  {{site.data.keyword.cos_short}} .</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>Opcional: o tipo de log do qual você deseja criar uma captura instantânea. Atualmente, `master` é a única opção, bem como a padrão.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Comando de exemplo**:

```
ibmcloud oc logging-collect --cluster mycluster --cos-bucket mybucket --cos-endpoint s3-api.us-geo.objectstorage.softlayer.net --hmac-key-id e2e7f5c9fo0144563c418dlhi3545m86 --hmac-key c485b9b9fo4376722f692b63743e65e1705301ab051em96j
```
{: pre}

**Saída de exemplo**:

```
Não há nenhum tipo de log especificado. O mestre padrão será usado.
Enviando a solicitação de coleção de logs para logs principais para o cluster mycluster... OK A solicitação de coleção de logs foi enviada com êxito. Para visualizar o status da solicitação, execute ibmcloud oc logging-collect-status mycluster.
```
{: screen}

</br>
### `ibmcloud oc logging-collect-status`
{: #cs_log_collect_status}

Verifique o status da solicitação de captura instantânea de coleção de logs para seu cluster.
{: shortdesc}



```
ibmcloud oc logging-collect-status --cluster CLUSTER [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Administrador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster para o qual você deseja criar uma captura instantânea. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Comando de exemplo**:

```
ibmcloud oc logging-collect-status --cluster mycluster
```
{: pre}

**Saída de exemplo**:

```
Getting the status of the last log collection request for cluster mycluster...
  OK
  State     Start Time             Error   Log URLs
  success   2018-09-18 16:49 PDT   - s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-0-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
  s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-1-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
  s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-2-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
```
{: screen}

</br>
### `ibmcloud oc logging-config-create`
{: #cs_logging_create}

Crie uma configuração de criação de log. É possível usar esse comando para encaminhar logs para contêineres, aplicativos, nós do trabalhador, clusters do Kubernetes e balanceadores de carga do aplicativo Ingress para o {{site.data.keyword.loganalysisshort_notm}} ou para um servidor syslog externo.
{: shortdesc}



```
ibmcloud oc logging-config-create --cluster CLUSTER --logsource LOG_SOURCE --type LOG_TYPE [--namespace KUBERNETES_NAMESPACE] [--hostname LOG_SERVER_HOSTNAME_OR_IP] [--port LOG_SERVER_PORT] [--space CLUSTER_SPACE] [--org CLUSTER_ORG] [--app-containers CONTAINERS] [--app-paths PATHS_TO_LOGS] [--syslog-protocol PROTOCOL]  [--json] [--skip-validation] [--force-update][-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster para todas as origens de log, exceto `kube-audit`, e a função da plataforma **Administrador** para o cluster para a origem de log `kube-audit`

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster.</dd>

<dt><code>--logsource <em>LOG_SOURCE</em></code></dt>
<dd>A origem do log para o qual ativar o encaminhamento de log. Esse argumento suporta uma lista separada por vírgula de origens de log a serem aplicadas para a configuração. Os valores aceitos são <code>container</code>, <code>application</code>, <code>worker</code>, <code>kubernetes</code>, <code>storage</code>, <code>ingress</code> e <code>kube-audit</code>. Se você não fornecer uma origem de log, configurações serão criadas para <code>container</code> e <code>ingress</code>.</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>Onde você deseja encaminhar os logs. As opções são <code>ibm</code>, que encaminha os logs para o {{site.data.keyword.loganalysisshort_notm}} e <code>syslog</code>, que encaminha os logs para um servidor externo.<p class="deprecated">O {{site.data.keyword.loganalysisshort_notm}} foi descontinuado. Essa opção de comando é suportada até 30 de setembro de 2019.</p></dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>O namespace do Kubernetes do qual você deseja encaminhar logs. O encaminhamento de log não é suportado para os namespaces do Kubernetes <code>ibm-system</code> e <code>kube-system</code>. Esse valor é válido somente para a origem de log do contêiner e é opcional. Se você não especificar um namespace, todos os namespaces no cluster usarão essa configuração.</dd>

<dt><code>--hostname <em>LOG_SERVER_HOSTNAME</em></code></dt>
<dd>Quando o tipo de criação de log for <code>syslog</code>, esse valor será o nome do host ou o endereço IP do servidor do coletor de log. Esse valor é necessário para <code>syslog</code>. Quando o tipo de criação de log é <code>ibm</code>, esse valor é a URL de ingestão do {{site.data.keyword.loganalysislong_notm}}. É possível localizar a lista de URLs de ingestão disponíveis
[aqui](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_ingestion#log_ingestion_urls). Se você não especificar uma URL de ingestão, o endpoint para a região na qual seu cluster foi criado será usado.</dd>

<dt><code>--port <em>LOG_SERVER_PORT</em></code></dt>
<dd>A porta do servidor coletor do log. Esse valor é opcional. Se você não especificar uma porta, a porta padrão <code>514</code> será usada para <code>syslog</code> e a porta padrão <code>9091</code> será usada para <code>ibm</code>.</dd>

<dt><code>--space <em>CLUSTER_SPACE</em></code></dt>
<dd>Opcional: o nome do espaço do Cloud Foundry para o qual você deseja enviar logs. Esse valor é válido somente para o tipo de log <code>ibm</code> e é opcional. Se você não especificar um espaço, os logs serão enviados para o nível de conta. Se você fizer isso, também deverá especificar uma <code>org</code>.</dd>

<dt><code>--org <em>CLUSTER_ORG</em></code></dt>
<dd>Opcional: o nome da organização do Cloud Foundry na qual o espaço estiver. Esse valor é válido somente para o tipo de log <code>ibm</code> e é necessário se você especificou um espaço.</dd>

<dt><code>--app-paths</code></dt>
<dd>O caminho no contêiner no qual os apps estão efetuando login. Para encaminhar logs com tipo de origem <code>application</code>, deve-se fornecer um caminho. Para especificar mais de um caminho, use uma lista separada por vírgula. Esse valor é necessário para origem de log <code>application</code>. Exemplo: <code>/var/log/myApp1/&ast;,/var/log/myApp2/&ast;</code></dd>

<dt><code>-- syslog-protocol</code></dt>
<dd>O protocolo de camada de transferência que será usado quando o tipo de criação de log for <code>syslog</code>. Os valores suportados são <code>tcp</code>, <code>tls</code> e o <code>udp</code> padrão. Ao encaminhar para um servidor rsyslog com o protocolo <code>udp</code>, os logs que têm mais de 1 KB são truncados.</dd>

<dt><code>--app-containers</code></dt>
<dd>Para encaminhar logs de apps, é possível especificar o nome do contêiner que contém o seu app. É possível especificar mais de um contêiner usando uma lista separada por vírgula. Se nenhum contêiner é especificado, os logs são encaminhados de todos os contêineres que contêm os caminhos que você forneceu. Essa opção é válida somente para a origem de log <code>application</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>--skip-validation</code></dt>
<dd>Ignore a validação dos nomes da organização e do espaço quando são especificados. Ignorar a validação diminui o tempo de processamento, mas uma configuração de criação de log inválida não encaminhará os logs corretamente. Esse valor é opcional.</dd>

<dt><code>--force-update</code></dt>
<dd>Force os seus pods do Fluentd para serem atualizados para a versão mais recente. O Fluentd deve estar na versão mais recente para mudar as configurações de criação de log.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplos**:

Exemplo para o tipo de log `syslog` que encaminha de uma origem de log `container` na porta padrão 514:
```
ibmcloud oc logging-config-create my_cluster --logsource container --namespace my_namespace  --hostname 169.xx.xxx.xxx --type syslog
```
{: pre}

Exemplo para o tipo de log `syslog` que encaminha logs de uma origem `ingress` em uma porta diferente do padrão:
```
ibmcloud oc logging-config-create --cluster my_cluster --logsource container --hostname 169.xx.xxx.xxx --port 5514 --type syslog
```
{: pre}

</br>
### `ibmcloud oc logging-config-get`
{: #cs_logging_get}

Visualize todas as configurações de encaminhamento de log para um cluster ou filtre configurações de criação de log com base em origem de log.
{: shortdesc}



```
ibmcloud oc logging-config-get --cluster CLUSTER [--logsource LOG_SOURCE] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--logsource <em>LOG_SOURCE</em></code></dt>
<dd>O tipo de origem de log para a qual você deseja filtrar. As configurações de criação de log de apenas essa origem de log no cluster são retornadas. Os valores aceitos são <code>container</code>, <code>storage</code>, <code>application</code>, <code>worker</code>, <code>kubernetes</code>, <code>ingress</code> e <code>kube-audit</code>. Esse valor é opcional.</dd>

<dt><code>--show-cobrindo-filtros</code></dt>
<dd>Mostra os filtros de criação de log que tornam os filtros prévios obsoletos.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc logging-config-get --cluster my_cluster --logsource worker
```
{: pre}

</br>
### `ibmcloud oc logging-config-refresh`
{: #cs_logging_refresh}

Atualize a configuração de criação de log para o cluster. Essa ação atualiza o token de criação de log para qualquer configuração de criação de log que está encaminhando para o nível de espaço em seu cluster.
{: shortdesc}



```
ibmcloud oc logging-config-refresh --cluster CLUSTER [--force-update] [-s]
```

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--force-update</code></dt>
<dd>Force os seus pods do Fluentd para serem atualizados para a versão mais recente. O Fluentd deve estar na versão mais recente para mudar as configurações de criação de log.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:

  ```
  ibmcloud oc logging-config-refresh --cluster my_cluster
  ```
  {: pre}

</br>
### `ibmcloud oc logging-config-rm`
{: #cs_logging_rm}

Excluir uma configuração de encaminhamento de log ou todas as configurações de criação de log para um cluster. A exclusão da configuração de log para o encaminhamento de log para um servidor syslog remoto ou para o {{site.data.keyword.loganalysisshort_notm}}.
{: shortdesc}



```
ibmcloud oc logging-config-rm --cluster CLUSTER [--id LOG_CONFIG_ID] [--all] [--force-update] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster para todas as origens de log, exceto `kube-audit`, e a função da plataforma **Administrador** para o cluster para a origem de log `kube-audit`

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--id <em>LOG_CONFIG_ID</em></code></dt>
<dd>Se você deseja remover uma configuração de criação de log única, o ID de configuração de criação de log.</dd>

<dt><code>--all</code></dt>
<dd>A sinalização para remover todas as configurações de criação de log em um cluster.</dd>

<dt><code>--force-update</code></dt>
<dd>Force os seus pods do Fluentd para serem atualizados para a versão mais recente. O Fluentd deve estar na versão mais recente para mudar as configurações de criação de log.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc logging-config-rm --cluster my_cluster --id f4bc77c0-ee7d-422d-aabf-a4e6b977264e
```
{: pre}

</br>
### `ibmcloud oc logging-config-update`
{: #cs_logging_update}

Atualize os detalhes de uma configuração de encaminhamento de log.
{: shortdesc}



```
ibmcloud oc logging-config-update --cluster CLUSTER --id LOG_CONFIG_ID --type LOG_TYPE  [--namespace NAMESPACE] [--hostname LOG_SERVER_HOSTNAME_OR_IP] [--port LOG_SERVER_PORT] [--space CLUSTER_SPACE] [--org CLUSTER_ORG] [--app-paths PATH] [--app-containers PATH] [--json] [--skipValidation] [--force-update] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--id <em>LOG_CONFIG_ID</em></code></dt>
<dd>O ID de configuração de criação de log que você deseja atualizar. Este valor é obrigatório.</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>O protocolo de encaminhamento de log que você deseja usar. Atualmente, <code>syslog</code> e <code>ibm</code> são suportados. Este valor é obrigatório.</dd>

<dt><code>--namespace <em>NAMESPACE</em></code>
<dd>O namespace do Kubernetes do qual você deseja encaminhar logs. O encaminhamento de log não é suportado para os namespaces do Kubernetes <code>ibm-system</code> e <code>kube-system</code>. Esse valor é válido somente para a origem de log do <code>container</code>. Se você não especificar um namespace, todos os namespaces no cluster usarão essa configuração.</dd>

<dt><code>--hostname <em>LOG_SERVER_HOSTNAME</em></code></dt>
<dd>Quando o tipo de criação de log for <code>syslog</code>, esse valor será o nome do host ou o endereço IP do servidor do coletor de log. Esse valor é necessário para <code>syslog</code>. Quando o tipo de criação de log é <code>ibm</code>, esse valor é a URL de ingestão do {{site.data.keyword.loganalysislong_notm}}. É possível localizar a lista de URLs de ingestão disponíveis
[aqui](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_ingestion#log_ingestion_urls). Se você não especificar uma URL de ingestão, o endpoint para a região na qual seu cluster foi criado será usado.</dd>

<dt><code>--port <em>LOG_SERVER_PORT</em></code></dt>
<dd>A porta do servidor coletor do log. Esse valor será opcional quando o tipo de criação de log for <code>syslog</code>. Se você não especificar uma porta, a porta padrão <code>514</code> será usada para <code>syslog</code> e <code>9091</code>
será usada para <code>ibm</code>.</dd>

<dt><code>--space <em>CLUSTER_SPACE</em></code></dt>
<dd>Opcional: o nome do espaço para o qual você deseja enviar logs. Esse valor é válido somente para o tipo de log <code>ibm</code> e é opcional. Se você não especificar um espaço, os logs serão enviados para o nível de conta. Se você fizer isso, também deverá especificar uma <code>org</code>.</dd>

<dt><code>--org <em>CLUSTER_ORG</em></code></dt>
<dd>Opcional: o nome da organização do Cloud Foundry na qual o espaço estiver. Esse valor é válido somente para o tipo de log <code>ibm</code> e é necessário se você especificou um espaço.</dd>

<dt><code>-- app-caminhos <em>PATH</em>,<em>PATH</em></code></dt>
<dd>Um caminho de arquivo absoluto no contêiner para coletar logs. Curingas, como '/var/log/*.log', podem ser usados, mas trechos recursivos, como '/var/log/**/test.log', não podem ser usados. Para especificar mais de um caminho, use uma lista separada por vírgula. Esse valor é obrigatório quando você especifica 'application' para a origem de log. </dd>

<dt><code>-- app-containers <em>PATH</em>,<em>PATH</em></code></dt>
<dd>O caminho nos contêineres nos quais os apps estão registrando. Para encaminhar logs com tipo de origem <code>application</code>, deve-se fornecer um caminho. Para especificar mais de um caminho, use uma lista separada por vírgula. Exemplo: <code>/var/log/myApp1/&ast;,/var/log/myApp2/&ast;</code></dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>--skipValidation</code></dt>
<dd>Ignore a validação dos nomes da organização e do espaço quando são especificados. Ignorar a validação diminui o tempo de processamento, mas uma configuração de criação de log inválida não encaminhará os logs corretamente. Esse valor é opcional.</dd>

<dt><code>--force-update</code></dt>
<dd>Force os seus pods do Fluentd para serem atualizados para a versão mais recente. O Fluentd deve estar na versão mais recente para mudar as configurações de criação de log.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo para o tipo de log `ibm`**:

  ```
  ibmcloud oc logging-config-update my_cluster --id f4bc77c0-ee7d-422d-aabf-a4e6b977264e --type ibm
  ```
  {: pre}

**Exemplo para o tipo de log `syslog`**:

  ```
  ibmcloud oc logging-config-update --cluster my_cluster --id f4bc77c0-ee7d-422d-aabf-a4e6b977264e --hostname localhost --port 5514 --type syslog
  ```
  {: pre}

</br>
### `ibmcloud oc logging-filter-create`
{: #cs_log_filter_create}

Filtre os logs que são encaminhados por sua configuração de criação de log.
{: shortdesc}



```
ibmcloud oc logging-filter-create --cluster CLUSTER --type LOG_TYPE [--logging-configs CONFIGS] [--namespace KUBERNETES_NAMESPACE] [--container CONTAINER_NAME] [--level LOGGING_LEVEL] [--message MESSAGE] [--regex-message MESSAGE] [--force-update] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster para o qual criar um filtro de criação de log. Este valor é obrigatório.</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>O tipo de logs nos quais você deseja aplicar o filtro. Atualmente <code>all</code>, <code>container</code> e <code>host</code> são suportados.</dd>

<dt><code>--logging-configs <em>CONFIGS</em></code></dt>
<dd>Uma lista separada por vírgulas de seus IDs de configuração de criação de log. Se não fornecido, o filtro será aplicado a todas as configurações de criação de log de cluster que forem passadas para o filtro. É possível visualizar as configurações de log que correspondem ao filtro usando a sinalização <code>--show-matching-configs</code> com o comando. Esse valor é opcional.</dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>O namespace do Kubernetes do qual se deseja filtrar logs. Esse valor é opcional.</dd>

<dt><code>--container <em>CONTAINER_NAME</em></code></dt>
<dd>O nome do contêiner do qual se deseja filtrar logs. Essa sinalização se aplicará apenas quando você estiver usando o tipo de log <code>container</code>. Esse valor é opcional.</dd>

<dt><code>--level <em>LOGGING_LEVEL</em></code></dt>
<dd>Filtra logs que estão no nível especificado e inferior. Os valores aceitáveis na ordem canônica são <code>fatal</code>, <code>error</code>, <code>warn/warning</code>, <code>info</code>, <code>debug</code> e <code>trace</code>. Esse valor é opcional. Como um exemplo, se você filtrou logs no nível <code>info</code>, <code>debug</code> e <code>trace</code> também serão filtrados. **Nota**: é possível usar essa sinalização apenas quando as mensagens de log estiverem em formato JSON e contiverem um campo de nível. Saída de exemplo: <code>{"log": "hello", "level": "info"}</code></dd>

<dt><code>--message <em>MESSAGE</em></code></dt>
<dd>Filtra quaisquer logs que contêm uma mensagem especificada em qualquer lugar no log. Esse valor é opcional. Exemplo: As mensagens "Hello", "!"e "Hello, World!"se aplicariam ao log "Hello, World!".</dd>

<dt><code>--regex-message <em>MESSAGE</em></code></dt>
<dd>Filtra quaisquer logs que contêm uma mensagem especificada que é gravada como uma expressão regular em qualquer lugar no log. Esse valor é opcional. Exemplo: o padrão "hello [0-9]" se aplicaria a "hello 1", "hello 2" e "hello 9".</dd>

<dt><code>--force-update</code></dt>
<dd>Force os seus pods do Fluentd para serem atualizados para a versão mais recente. O Fluentd deve estar na versão mais recente para mudar as configurações de criação de log.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplos**:

Este exemplo filtra todos os logs que são encaminhados de contêineres com o nome `test-container` no namespace padrão que estão no nível de depuração ou menos e têm uma mensagem de log que contém "solicitação GET".
```
ibmcloud oc logging-filter-create --cluster example-cluster --type container --namespace default --container test-container --level debug --message "GET request"
```
{: pre}

Este exemplo filtra todos os logs que são encaminhados, em um nível <code>info</code> ou inferior, de um cluster específico. A saída é retornada como JSON.
```
ibmcloud oc logging-filter-create --cluster example-cluster --type all --level info --json
```
{: pre}

</br>
### `ibmcloud oc logging-filter-get`
{: #cs_log_filter_view}

Visualize uma configuração de filtro de criação de log.
{: shortdesc}



```
ibmcloud oc logging-filter-get --cluster CLUSTER [--id FILTER_ID] [--show-matching-configs] [--show-covering-filters] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster do qual você deseja visualizar filtros. Este valor é obrigatório.</dd>

<dt><code>--id <em>FILTER_ID</em></code></dt>
<dd>O ID do filtro de log que você deseja visualizar.</dd>

<dt><code>--show-matching-configs</code></dt>
<dd>Mostre as configurações de criação de log que correspondem à configuração que você está visualizando. Esse valor é opcional.</dd>

<dt><code>--show-cobrindo-filtros</code></dt>
<dd>Mostre os filtros de criação de log que tornam os filtros prévios obsoletos. Esse valor é opcional.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc logging-filter-get --cluster mycluster --id 885732 --show-matching-configs
```
{: pre}

</br>
### `ibmcloud oc logging-filter-rm`
{: #cs_log_filter_delete}

Exclua um filtro de criação de log
{: shortdesc}



```
ibmcloud oc logging-filter-rm --cluster CLUSTER [--id FILTER_ID] [--all] [--force-update] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster por meio do qual você deseja excluir um filtro.</dd>

<dt><code>--id <em>FILTER_ID</em></code></dt>
<dd>O ID do filtro de log a ser excluído.</dd>

<dt><code>--all</code></dt>
<dd>Exclua todos os seus filtros de encaminhamento de log. Esse valor é opcional.</dd>

<dt><code>--force-update</code></dt>
<dd>Force os seus pods do Fluentd para serem atualizados para a versão mais recente. O Fluentd deve estar na versão mais recente para mudar as configurações de criação de log.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc logging-filter-rm --cluster mycluster --id 885732
```
{: pre}

</br>
### `ibmcloud oc logging-filter-update`
{: #cs_log_filter_update}

Atualize um filtro de criação de log.
{: shortdesc}



```
ibmcloud oc logging-filter-update --cluster CLUSTER --id FILTER_ID --type LOG_TYPE [--logging-configs CONFIGS] [--namespace KUBERNETES_NAMESPACE] [--container CONTAINER_NAME] [--level LOGGING_LEVEL] [--message MESSAGE] [--regex-message MESSAGE] [--force-update] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster para o qual você deseja atualizar um filtro de criação de log. Este valor é obrigatório.</dd>

<dt><code>--id <em>FILTER_ID</em></code></dt>
<dd>O ID do filtro de log a ser atualizado.</dd>

<dt><code>--type <em>LOG_TYPE</em></code></dt>
<dd>O tipo de logs nos quais você deseja aplicar o filtro. Atualmente <code>all</code>, <code>container</code> e <code>host</code> são suportados.</dd>

<dt><code>--logging-configs <em>CONFIGS</em></code></dt>
<dd>Uma lista separada por vírgulas de seus IDs de configuração de criação de log. Se não fornecido, o filtro será aplicado a todas as configurações de criação de log de cluster que forem passadas para o filtro. É possível visualizar as configurações de log que correspondem ao filtro usando a sinalização <code>--show-matching-configs</code> com o comando. Esse valor é opcional.</dd>

<dt><code>--namespace <em>KUBERNETES_NAMESPACE</em></code></dt>
<dd>O namespace do Kubernetes do qual se deseja filtrar logs. Esse valor é opcional.</dd>

<dt><code>--container <em>CONTAINER_NAME</em></code></dt>
<dd>O nome do contêiner do qual se deseja filtrar logs. Essa sinalização se aplicará apenas quando você estiver usando o tipo de log <code>container</code>. Esse valor é opcional.</dd>

<dt><code>--level <em>LOGGING_LEVEL</em></code></dt>
<dd>Filtra logs que estão no nível especificado e inferior. Os valores aceitáveis na ordem canônica são <code>fatal</code>, <code>error</code>, <code>warn/warning</code>, <code>info</code>, <code>debug</code> e <code>trace</code>. Esse valor é opcional. Como um exemplo, se você filtrou logs no nível <code>info</code>, <code>debug</code> e <code>trace</code> também serão filtrados. **Nota**: é possível usar essa sinalização apenas quando as mensagens de log estiverem em formato JSON e contiverem um campo de nível. Saída de exemplo: <code>{"log": "hello", "level": "info"}</code></dd>

<dt><code>--message <em>MESSAGE</em></code></dt>
<dd>Filtra quaisquer logs que contêm uma mensagem especificada em qualquer lugar no log. Esse valor é opcional. Exemplo: As mensagens "Hello", "!"e "Hello, World!"se aplicariam ao log "Hello, World!".</dd>

<dt><code>--regex-message <em>MESSAGE</em></code></dt>
<dd>Filtra quaisquer logs que contêm uma mensagem especificada que é gravada como uma expressão regular em qualquer lugar no log. Esse valor é opcional. Exemplo: o padrão "hello [0-9]" se aplicaria a "hello 1", "hello 2" e "hello 9"</dd>

<dt><code>--force-update</code></dt>
<dd>Force os seus pods do Fluentd para serem atualizados para a versão mais recente. O Fluentd deve estar na versão mais recente para mudar as configurações de criação de log.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplos**:

Este exemplo filtra todos os logs que são encaminhados de contêineres com o nome `test-container` no namespace padrão que estão no nível de depuração ou menos e têm uma mensagem de log que contém "solicitação GET".
```
ibmcloud oc logging-filter-update --cluster example-cluster --id 885274 --type container --namespace default --container test-container --level debug --message "GET request"
```
{: pre}

Este exemplo filtra todos os logs que são encaminhados, em um nível <code>info</code> ou inferior, de um cluster específico. A saída é retornada como JSON.
```
ibmcloud oc logging-filter-update --cluster example-cluster --id 274885 --type all --level info --json
```
{: pre}

<br />


## Comandos do balanceador de carga de rede (NLB)
{: #nlb-dns}

Use esse grupo de comandos para criar e gerenciar nomes de host para endereços IP do balanceador de carga de rede (NLB) e monitores de verificação de funcionamento para nomes de host. Para obter mais informações, consulte [Registrando um nome de host de balanceador de carga](/docs/containers?topic=containers-loadbalancer_hostname).
{: shortdesc}



### `ibmcloud oc nlb-dns-add`
{: #cs_nlb-dns-add}

Inclua um IP de balanceador de carga de rede (NLB) em um nome do host existente que você criou com o [comando `ibmcloud oc nlb-dns-create`](#cs_nlb-dns-create).
{: shortdesc}



Por exemplo, é possível criar um NLB em cada zona de um cluster multizona para expor um aplicativo. Você registra um IP do NLB em uma zona com um nome do host executando `ibmcloud oc nlb-dns-create`, portanto, agora é possível incluir os IPs do NLB de outras zonas nesse nome do host existente. Quando um usuário acessa o seu nome do host do app, o cliente acessa um desses IPs aleatoriamente e a solicitação é enviada para esse NLB. Deve-se executar o comando a seguir para cada endereço IP que você deseja incluir.

```
ibmcloud oc nlb-dns-add --cluster CLUSTER --ip IP --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--ip <em>IP</em></code></dt>
<dd>O IP do NLB que você deseja incluir no nome do host. Para ver seus IPs do NLB, execute <code>oc get svc</code>.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>O nome de host no qual você deseja incluir IPs. Para ver os nomes do host existentes, execute <code>ibmcloud oc nlb-dnss</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dns-add --cluster mycluster --ip 1.1.1.1 --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-create`
{: #cs_nlb-dns-create}

Exponha seu aplicativo publicamente criando um nome de host DNS para registrar um IP de balanceador de carga de rede (NLB).
{: shortdesc}



```
ibmcloud oc nlb-dns-create --cluster CLUSTER --ip IP [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--ip <em>IP</em></code></dt>
<dd>O endereço IP do balanceador de carga de rede que você deseja registrar. Para ver seus IPs do NLB, execute <code>oc get svc</code>. É possível criar inicialmente o nome do host com apenas um endereço IP. Se você tiver NLBs em cada zona de um cluster de várias zonas que exponham um app, será possível incluir os IPs dos outros NLBs no nome do host executando o [comando `ibmcloud oc nlb-dns-add`](#cs_nlb-dns-add).</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dns-create --cluster mycluster --ip 1.1.1.1
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-rm`
{: #cs_nlb-dns-rm}

Remova um endereço IP de balanceador de carga de rede de um nome de host. Se você remover todos os IPs de um nome do host, o nome do host ainda existirá, mas nenhum IP será associado a ele. <strong>Nota</strong>: deve-se executar esse comando para cada endereço IP que você deseja remover.
{: shortdesc}



```
ibmcloud oc nlb-dns-rm --cluster CLUSTER --ip IP --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--ip <em>IP</em></code></dt>
<dd>O IP do NLB que você deseja remover. Para ver seus IPs do NLB, execute <code>oc get svc</code>.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>O nome de host do qual você deseja remover um IP. Para ver os nomes do host existentes, execute <code>ibmcloud oc nlb-dnss</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dns-rm --cluster mycluster --ip 1.1.1.1 --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>
### `ibmcloud oc nlb-dnss`
{: #cs_nlb-dns-ls}

Liste os nomes de host e os endereços IP do balanceador de carga de rede registrados em um cluster.
{: shortdesc}



```
ibmcloud oc nlb-dnss --cluster CLUSTER [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dnss --cluster mycluster
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-monitor-configure`
{: #cs_nlb-dns-monitor-configure}

Configure e, opcionalmente, ative um monitor de verificação de funcionamento para um nome de host do NLB existente em um cluster. Quando você ativa um monitor para seu nome de host, ele verifica o funcionamento do IP do NLB em cada zona e mantém os resultados da consulta de DNS atualizados com base nessas verificações de funcionamento.
{: shortdesc}

É possível usar esse comando para criar e ativar um novo monitor de verificação de funcionamento ou para atualizar as configurações para um monitor de verificação de funcionamento existente. Para criar um novo monitor, inclua o sinalizador `-- enable` e os sinalizadores para todas as configurações que deseja definir. Para atualizar um monitor existente, inclua apenas os sinalizadores para as configurações que deseja mudar.



```
ibmcloud oc nlb-dns-monitor-configure --cluster CLUSTER --nlb-host HOST NAME [--enable] [--desc DESCRIPTION] [--type TYPE] [--method METHOD] [--path PATH] [--timeout TIMEOUT] [--retries RETRIES] [--interval INTERVAL] [--port PORT] [--header HEADER] [--expected-body BODY STRING] [--expected-codes HTTP CODES] [--follows-redirects TRUE] [--allows-insecure TRUE] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster no qual o nome de host está registrado.</dd>

<dt><code>--nlb-host <em>HOST NAME</em></code></dt>
<dd>O nome de host para o qual configurar um monitor de verificação de funcionamento. Para listar os nomes do host, execute <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--enable</code></dt>
<dd>Inclua esse sinalizador para criar e ativar um novo monitor de verificação de funcionamento para um nome de host.</dd>

<dt><code>--description <em>DESCRIPTION</em></code></dt>
<dd>Uma descrição do monitor de funcionamento.</dd>

<dt><code>--type <em>TYPE</em></code></dt>
<dd>O protocolo a ser usado para a verificação de funcionamento: <code>HTTP</code>, <code>HTTPS</code> ou <code>TCP</code>. Padrão: <code>HTTP</code></dd>

<dt><code>--method <em>METHOD</em></code></dt>
<dd>O método a ser usado para a verificação de funcionamento. Padrão para <code>type</code> <code>HTTP</code> e <code>HTTPS</code>: <code>GET</code>. Padrão para <code>type</code> <code>TCP</code>: <code>connection_established</code>.</dd>

<dt><code>--path <em>PATH</em></code></dt>
<dd>Quando <code>type</code> for <code>HTTPS</code>: o caminho de terminal com relação ao qual será feita a verificação de funcionamento. Padrão: <code>/</code></dd>

<dt><code>--timeout <em>TIMEOUT</em></code></dt>
<dd>O tempo limite, em segundos, antes de o IP ser considerado inatingível. A verificação de funcionamento aguarda o número de segundos especificado no parâmetro `interval` antes de tentar atingir o IP novamente. O valor deve ser um número inteiro no intervalo de 1 a 15. Padrão: <code>5</code></dd>

<dt><code>--retries <em>RETRIES</em></code></dt>
<dd>Quando ocorre um tempo limite, o número de novas tentativas a serem tentadas antes de o IP inalcançável ser considerado não funcional. Novas tentativas são tentadas imediatamente. O valor deve ser um número inteiro no intervalo de 1 a 5. Padrão: <code>2</code></dd>

<dt><code>--interval <em>INTERVAL</em></code></dt>
<dd>O intervalo, em segundos, entre cada verificação de funcionamento. Intervalos curtos podem melhorar o tempo de failover, mas aumentar o carregamento nos IPs. O valor deve ser um número inteiro no intervalo de 10 a 3600 e deve ser maior que `(RETRIES + 1) * TIMEOUT`. Padrão: <code>60</code></dd>

<dt><code>--port <em>PORT</em></code></dt>
<dd>O número da porta à qual se conectar para a verificação de funcionamento. Quando <code>type</code> for <code>TCP</code>, esse parâmetro será necessário. Quando <code>type</code> for <code>HTTP</code> ou <code>HTTPS</code>, defina a porta somente se você usar uma porta diferente de 80 para HTTP ou 443 para HTTPS. Padrão para TCP: <code>0</code>. Padrão para HTTP: <code>80</code>. Padrão para HTTPS: <code>443</code>.</dd>

<dt><code>--header <em>HEADER</em></code></dt>
<dd>Quando <code>type</code> é <code>HTTPS</code> ou <code>HTTPS</code>: os cabeçalhos da solicitação de HTTP a serem enviados na verificação de funcionamento, como um cabeçalho de Host. Não é possível substituir o cabeçalho do Agente do Usuário.</dd>

<dt><code>--expected-body <em>BODY STRING</em></code></dt>
<dd>Quando <code>type</code> for <code>HTTP</code> ou <code>HTTPS</code>: uma subsequência sem distinção entre maiúsculas e minúsculas que a verificação de funcionamento procurará no corpo da resposta. Se essa sequência não for localizada, o IP será considerado não funcional.</dd>

<dt><code>--expected-codes <em>HTTP CODES</em></code></dt>
<dd>Quando <code>type</code> for <code>HTTP</code> ou <code>HTTPS</code>: códigos de HTTP que a verificação de funcionamento procurará na resposta. Se o código de HTTP não for localizado, o IP será considerado não funcional. Padrão: <code>2xx</code></dd>

<dt><code>--allows-insecure <em>TRUE</em></code></dt>
<dd>Quando <code>type</code> for <code>HTTP</code> ou <code>HTTPS</code>: configure como <code>true</code> para não validar o certificado.</dd>

<dt><code>--follows-redirects <em>TRUE</em></code></dt>
<dd>Quando <code>type</code> for <code>HTTP</code> ou <code>HTTPS</code>: configure como <code>true</code> para seguir quaisquer redirecionamentos que forem retornados pelo IP.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dns-monitor-configure --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud --enable --desc "Login page monitor" --type HTTPS --method GET --path / --timeout 5 --retries 2 --interval 60  --expected-body "healthy" --expected-codes 2xx --follows-redirects true
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-monitor-disable`
{: #cs_nlb-dns-monitor-disable}

Desativar um monitor de verificação de funcionamento existente para um nome do host em um cluster.
{: shortdesc}



```
ibmcloud oc nlb-dns-monitor-disable --cluster CLUSTER --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>O nome do host que o funcionamento do monitor verifica. Para listar os nomes do host, execute <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dns-monitor-disable --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-monitor-enable`
{: #cs_nlb-dns-monitor-enable}

Ative um monitor de verificação de funcionamento que você configurou.
{: shortdesc}

Na primeira vez que você cria um monitor de verificação de funcionamento, deve-se configurar e ativá-lo com o comando `ibmcloud oc nlb-dns-monitor-configure`. Use o comando `ibmcloud oc nlb-dns-monitor-enable` somente para ativar um monitor que você configurou, mas ainda não ativou, ou para reativar um monitor que você desativou anteriormente.



```
ibmcloud oc nlb-dns-monitor-enable --cluster CLUSTER --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>O nome do host que o funcionamento do monitor verifica. Para listar os nomes do host, execute <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dns-monitor-enable --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>

### `ibmcloud oc nlb-dns-monitor-get`
{: #cs_nlb-dns-monitor-get}

Visualize as configurações para um monitor de verificação de funcionamento existente.
{: shortdesc}



```
ibmcloud oc nlb-dns-monitor-get --cluster CLUSTER --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>O nome do host que o funcionamento do monitor verifica. Para listar os nomes do host, execute <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dns-monitor-get --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>

### `ibmcloud oc nlb-dns-monitor-status`
{: #cs_nlb-dns-monitor-status}

Liste o status de verificação de funcionamento para os IPs atrás de nomes de host do NLB em um cluster.
{: shortdesc}



```
ibmcloud oc nlb-dns-monitor-status --cluster CLUSTER [--nlb-host HOST_NAME] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Inclua esse sinalizador para visualizar o status para apenas um nome de host. Para listar os nomes do host, execute <code>ibmcloud oc nlb-dnss --cluster CLUSTER</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dns-monitor-status --cluster mycluster
```
{: pre}

</br>
### `ibmcloud oc nlb-dns-monitors`
{: #cs_nlb-dns-monitor-ls}

Liste as configurações do monitor de verificação de funcionamento para cada nome de host do NLB em um cluster.
{: shortdesc}



```
ibmcloud oc nlb-dns-monitors --cluster CLUSTER [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Editor** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc nlb-dns-monitors --cluster mycluster
```
{: pre}

<br />


## Comandos de região e localização
{: #region_commands}

Use esse grupo de comandos para visualizar locais disponíveis e para visualizar e configurar a região de destino atual.
{: shortdesc}

### Descontinuado: `ibmcloud oc region-get`
{: #cs_region}

Localize a região de destino atual do {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

Será possível trabalhar com recursos aos quais você tem acesso em qualquer localização, mesmo se você configurar uma região executando `ibmcloud oc region-set` e o recurso com o qual você desejar trabalhar estiver em outra região. Se você tiver clusters com o mesmo nome em diferentes regiões, será possível usar o ID do cluster quando executar comandos ou configurar uma região com o comando `ibmcloud oc region-set` e usar o nome do cluster quando executar comandos.

<p class="deprecated">Comportamento anterior:</br> se você usar a versão <code>0.3</code> ou mais recente do plug-in do {{site.data.keyword.containerlong_notm}} e precisar listar e trabalhar com recursos de uma região apenas, será possível usar o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_init) <code>ibmcloud oc init</code> para ter como destino um terminal regional em vez do terminal global. </br>Se você [configurar a variável de ambiente <code>IKS_BETA_VERSION</code> no plug-in do {{site.data.keyword.containerlong_notm}} como <code>0.2</code>](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_beta), você criará e gerenciará clusters específicos para a região. Use o comando <code>ibmcloud oc region-set</code> para mudar regiões.</p>

```
ibmcloud oc region-get
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

</br>
### Descontinuado: `ibmcloud oc region-set`
{: #cs_region-set}

Configure a região para o  {{site.data.keyword.containerlong_notm}}.
{: shortdesc}

Será possível trabalhar com recursos aos quais você tem acesso em qualquer localização, mesmo se você configurar uma região executando `ibmcloud oc region-set` e o recurso com o qual você desejar trabalhar estiver em outra região. Se você tiver clusters com o mesmo nome em diferentes regiões, será possível usar o ID do cluster quando executar comandos ou configurar uma região com o comando `ibmcloud oc region-set` e usar o nome do cluster quando executar comandos.

Se usar a versão beta `0.2` (anterior) do plug-in do {{site.data.keyword.containerlong_notm}}, você criará e gerenciará clusters específicos para a região. Por exemplo, é possível efetuar login no {{site.data.keyword.cloud_notm}} na região sul dos EUA e criar um cluster. Em seguida, é possível usar `ibmcloud oc region-set eu-central` para ter a região central da UE como destino e criar outro cluster. Por fim, é possível usar `ibmcloud oc region-set us-south` para retornar para o sul dos EUA para gerenciar seu cluster nessa região.
{: deprecated}

```
ibmcloud oc region-set --region REGION
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

**Opções de comando**:
<dl>
<dt><code> -- region  <em> REGION </em> </code></dt>
<dd>Insira a região que você deseja destinar. Esse valor é opcional. Se você não fornecer a região, será possível selecionar uma na lista na saída.

Para obter uma lista de regiões disponíveis, revise as [Localizações](/docs/containers?topic=containers-regions-and-zones) ou use o [comando](#cs_regions) `ibmcloud oc regions`.</dd></dl>

**Exemplo**:
```
ibmcloud oc region-set --region eu-central
```
{: pre}

</br>
### Descontinuado: `ibmcloud oc regions`
{: #cs_regions}

Liste as regiões disponíveis. O `Region Name` é o nome do {{site.data.keyword.containerlong_notm}} e o `Region Alias` é o nome geral do {{site.data.keyword.cloud_notm}} para a região.
{: shortdesc}

Os terminais específicos da região foram descontinuados. Em vez disso, use o [terminal global](/docs/containers?topic=containers-regions-and-zones#endpoint).
{: deprecated}

** Permissões mínimas necessárias **: nenhuma

**Exemplo**:
```
ibmcloud oc regions
```
{: pre}

**Saída**:
```
Region Name   Region Alias
ap-north      jp-tok
ap-south      au-syd
eu-central    eu-de
uk-south      eu-gb
us-east       us-east
us-south      us-south
```
{: screen}

</br>
### `ibmcloud oc supported-locations`
{: #cs_supported-locations}

Liste os locais que são suportados pelo {{site.data.keyword.containerlong_notm}}. Para obter mais informações sobre os locais que são retornados, consulte [Locais do {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-regions-and-zones#locations).
{: shortdesc}



```
ibmcloud oc supported-locations
```
{: pre}

** Permissões mínimas necessárias **: nenhuma

</br>
### `ibmcloud oc zones`
{: #cs_datacenters}

Visualize uma lista de zonas disponíveis nas quais é possível criar um cluster.
{: shortdesc}



Se usar a versão beta `0.2` (anterior) do plug-in do {{site.data.keyword.containerlong_notm}}, as zonas disponíveis variarão de acordo com a região na qual você está com login efetuado. Para alternar regiões, execute `ibmcloud oc region-set`.
{: deprecated}

```
ibmcloud oc zones [--locations LOCATION] [--region-only] [--json] [-s]
```
{: pre}

**Permissões mínimas**: nenhuma

**Opções de comando**:
<dl>
<dt><code>--locations <em>LOCATION</em></code></dt>
<dd>Filtre zonas por um local específico ou uma lista de locais separados por vírgula. Para ver as localizações suportadas, execute <code>ibmcloud oc supported-locations</code>.</dd>

<dt><code> -- region-only </code></dt>
<dd>Liste as multizonas somente dentro da região para a qual você efetuou login. Esse valor é opcional.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc zones --locations ap
```
{: pre}

<br />



## Comandos de nó do trabalhador
{: worker_node_commands}

### Descontinuado: `ibmcloud oc worker-add`
{: #cs_worker_add}

Inclua nós do trabalhador independentes em um cluster.
{: shortdesc}

Esse comando foi descontinuado. Crie um conjunto de trabalhadores executando [`ibmcloud oc worker-pool-create`](#cs_worker_pool_create) ou inclua trabalhadores em um conjunto de trabalhadores existente executando [`ibmcloud oc worker-pool-resize`](#cs_worker_pool_resize).
{: deprecated}

```
ibmcloud oc worker-add --cluster CLUSTER [--file FILE_LOCATION] [--hardware HARDWARE] --machine-type MACHINE_TYPE --workers NUMBER --private-vlan PRIVATE_VLAN --public-vlan PUBLIC_VLAN [--disable-disk-encrypt] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--file <em>FILE_LOCATION</em></code></dt>
<dd>O caminho para o arquivo YAML incluir nós do trabalhador no cluster. Em vez de definir nós do trabalhador adicionais usando as opções fornecidas nesse comando, será possível usar um arquivo do YAML. Esse valor é opcional.

<p class="note">Se, no comando, você fornecer a mesma opção que o parâmetro no arquivo YAML, o valor no comando terá precedência sobre o valor no YAML. Por exemplo, você define um tipo em seu arquivo YAML e usa a opção <code>--machine-type</code> no comando e o valor que você inseriu na opção de comando substitui o valor no arquivo YAML.</p>

<pre class="codeblock">
<code>name: <em>&lt;cluster_name_or_ID&gt;</em>
zone: <em>&lt;zone&gt;</em>
machine-type: <em>&lt;machine_type&gt;</em>
private-vlan: <em>&lt;private_VLAN&gt;</em>
public-vlan: <em>&lt;public_VLAN&gt;</em>
hardware: <em>&lt;shared_or_dedicated&gt;</em>
workerNum: <em>&lt;number_workers&gt;</em>
diskEncryption: <em>false</em></code></pre>

<table>
<caption>Entendendo os componentes de arquivo YAML</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ícone de ideia"/> entendendo os componentes de arquivo do YAML</th>
</thead>
<tbody>
<tr>
<td><code><em>name</em></code></td>
<td>Substitua <code><em>&lt;cluster_name_or_ID&gt;</em></code> pelo nome ou ID do cluster no qual você deseja incluir nós do trabalhador.</td>
</tr>
<tr>
<td><code><em>zone</em></code></td>
<td>Substitua <code><em>&lt;zone&gt;</em></code> pela zona para implementar os seus nós do trabalhador. As zonas disponíveis dependem da região em que você efetuou login. Para listar as zonas disponíveis, execute <code>ibmcloud oc zones</code>.</td>
</tr>
<tr>
<td><code><em>machine-type</em></code></td>
<td>Substitua <code><em>&lt;machine_type&gt;</em></code> pelo tipo, ou o tipo de máquina, para a qual você deseja implementar os nós do trabalhador. É possível implementar os nós do trabalhador como máquinas virtuais em hardware compartilhado ou dedicado ou como máquinas físicas no bare metal. Os tipos físicos e virtuais disponíveis variam de acordo com a zona na qual você implementa o cluster. Para obter mais informações, consulte o [comando](#cs_machine_types) `ibmcloud oc flavors (machine-types)`.</td>
</tr>
<tr>
<td><code><em>private-vlan</em></code></td>
<td>Substitua <code><em>&lt;private_VLAN&gt;</em></code> pelo ID da VLAN privada que você deseja usar para os seus nós do trabalhador. Para listar as VLANs disponíveis, execute <code>ibmcloud oc vlans --zone <em>&lt;zone&gt;</em></code> e procure por roteadores de VLAN que começam com <code>bcr</code> (roteador de back-end).</td>
</tr>
<tr>
<td><code>public-vlan</code></td>
<td>Substitua <code>&lt;public_VLAN&gt;</code> pelo ID da VLAN pública que você deseja usar para os seus nós do trabalhador. Para listar as VLANs disponíveis, execute <code>ibmcloud oc vlans --zone &lt;zone&gt;</code> e procure por roteadores de VLAN que começam com <code>fcr</code> (roteador de front-end). <br><strong>Nota</strong>: Se os nós do trabalhador forem configurados apenas com uma VLAN privada, você deverá permitir que os nós do trabalhador e o cluster principal se comuniquem por [ativação do terminal em serviço privado](/docs/containers?topic=containers-cs_network_cluster#set-up-private-se) ou [configurando um dispositivo de gateway](/docs/containers?topic=containers-plan_clusters#workeruser-master).</td>
</tr>
<tr>
<td><code>hardware</code></td>
<td>Para os tipos virtuais: o nível de isolamento de hardware para o nó do trabalhador. Use `dedicated` para que os recursos físicos disponíveis que são dedicados apenas a você, ou `shared` para permitir que recursos físicos sejam compartilhados com outros clientes IBM. O padrão é `shared`.</td>
</tr>
<tr>
<td><code>workerNum</code></td>
<td>Substitua <code><em>&lt;number_workers&gt;</em></code> pelo número de nós do trabalhador que você deseja implementar.</td>
</tr>
<tr>
<td><code>diskEncryption: <em>false</em></code></td>
<td>Os nós do trabalhador apresentam criptografia de disco AES de 256 bits por padrão; [saiba mais](/docs/containers?topic=containers-security#encrypted_disk). Para desativar a criptografia, inclua essa opção e configure o valor para <code>false</code>.</td></tr>
</tbody></table></p></dd>

<dt><code>--hardware <em>HARDWARE</em></code></dt>
<dd>O nível de isolamento de hardware para seu nó do trabalhador. Use `dedicated` para que os recursos físicos disponíveis sejam dedicados apenas a você ou `shared` para permitir que recursos físicos sejam compartilhados com outros clientes IBM. O padrão é `shared`. Esse valor é opcional. Para os tipos bare metal, especifique `dedicated`.</dd>

<dt><code>--machine-type <em>MACHINE_TYPE</em></code></dt>
<dd>Escolha um tipo de máquina, ou tipo, para os nós do trabalhador. É possível implementar os nós do trabalhador como máquinas virtuais em hardware compartilhado ou dedicado ou como máquinas físicas no bare metal. Os tipos de máquinas físicas e virtuais disponíveis variam de acordo com a zona na qual você implementa o cluster. Para obter mais informações, consulte a documentação para o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_machine_types) `ibmcloud oc flavors (machine-types)`. Esse valor é necessário para clusters padrão e não está disponível para clusters livres.</dd>

<dt><code>--workers <em>NUMBER</em></code></dt>
<dd>Um número inteiro que representa o número de nós do trabalhador a serem criados no cluster. O valor padrão é 1. Esse valor é opcional.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>A VLAN privada que foi especificada quando o cluster foi criado. Este valor é obrigatório. Os roteadores de VLAN privada sempre iniciam com <code>bcr</code> (roteador de backend) e roteadores de VLAN pública sempre iniciam com <code>fcr</code> (roteador de front-end). Ao criar um cluster e especificar as VLANs públicas e privadas, a combinação de número e letra após esses prefixos devem corresponder.</dd>

<dt><code>--public-vlan <em>PUBLIC_VLAN</em></code></dt>
<dd>A VLAN pública que foi especificada quando o cluster foi criado. Esse valor é opcional. Se você deseja que os nós do trabalhador existam somente em uma VLAN privada, não forneça um ID de VLAN pública. Os roteadores de VLAN privada sempre iniciam com <code>bcr</code> (roteador de backend) e roteadores de VLAN pública sempre iniciam com <code>fcr</code> (roteador de front-end). Ao criar um cluster e especificar as VLANs públicas e privadas, a combinação de número e letra após esses prefixos devem corresponder.<p class="note">Se os nós do trabalhador estão configurados somente com uma VLAN privada, deve-se permitir que os nós do trabalhador e o cluster mestre se comuniquem [ativando o terminal em serviço privado](/docs/containers?topic=containers-cs_network_cluster#set-up-private-se) ou [configurando um dispositivo de gateway](/docs/containers?topic=containers-plan_clusters#workeruser-master).</p></dd>

<dt><code>--disable-disk-encrypt</code></dt>
<dd>Os nós do trabalhador apresentam criptografia de disco AES de 256 bits por padrão; [saiba mais](/docs/containers?topic=containers-security#encrypted_disk). Para desativar a criptografia, inclua essa opção.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>

</dl>

**Exemplo**:
```
ibmcloud oc worker-add --cluster my_cluster --workers 3 --public-vlan my_public_VLAN_ID --private-vlan my_private_VLAN_ID --machine-type b3c.4x16 --hardware shared
```
{: pre}

</br>
### `ibmcloud oc worker-get`
{: #cs_worker_get}

Visualize os detalhes de um nó do trabalhador.
{: shortdesc}



```
ibmcloud oc worker-get --cluster CLUSTER_NAME_OR_ID --worker WORKER_NODE_ID [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>-- cluster <em>CLUSTER_NAME_OR_ID</em></code></dt>
<dd>O nome ou o ID do cluster do nó do trabalhador. Esse valor é opcional.</dd>

<dt><code> -- worker  <em> WORKER_NODE_ID </em> </code></dt>
<dd>O nome do seu nó do trabalhador. Execute <code>ibmcloud oc workers --cluster <em>CLUSTER</em></code> para visualizar os IDs para os nós do trabalhador em um cluster. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-get --cluster my_cluster --worker kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1
```
{: pre}

**Saída de exemplo**:

  ```
  ID: kube-dal10-123456789-w1 State: normal Status: Ready Trust: disabled Private VLAN: 223xxxx Public VLAN: 223xxxx Private IP: 10.xxx.xx.xxx Public IP: 169.xx.xxx.xxx Hardware: shared Zone: dal10 Version: 1.8.11_1509
  ```
  {: screen}

</br>
### `ibmcloud oc worker-reboot`
{: #cs_worker_reboot}

Reinicialize um nó do trabalhador em um cluster.
{: shortdesc}



Durante a reinicialização, o estado do nó do trabalhador não muda. Por exemplo, você poderá usar uma reinicialização se o status do nó do trabalhador na infraestrutura do IBM Cloud for `Powered Off` e você precisar ativar o nó do trabalhador. Uma reinicialização limpa os diretórios temporários, mas não limpa o sistema de arquivos inteiro ou reformata os discos. O endereço IP do nó do trabalhador permanece o mesmo após a operação de reinicialização.

Reinicializar um nó do trabalhador pode causar distorção de dados no nó do trabalhador. Use esse comando com cuidado e quando souber que uma reinicialização pode ajudar a recuperar seu nó do trabalhador. Em todos os outros casos, [recarregue seu nó do trabalhador](#cs_worker_reload).
{: important}

Antes de reinicializar seu nó do trabalhador, certifique-se de que os pods sejam reprogramados em outros nós do trabalhador para ajudar a evitar o tempo de inatividade para seu aplicativo ou distorção de dados em seu nó do trabalhador.

1. Liste todos os nós do trabalhador em seu cluster e anote o **nome** do nó do trabalhador que você deseja remover.
   ```
   oc get nodes
   ```
   {: pre}
   O **nome** retornado nesse comando é o endereço IP privado designado ao nó do trabalhador. É possível localizar mais informações sobre seu nó do trabalhador ao executar o comando `ibmcloud oc workers --cluster <cluster_name_or_ID>` e procurar pelo nó do trabalhador com o mesmo endereço **IP privado**.

2. Marque o nó do trabalhador como não programável em um processo conhecido como bloqueio. Ao bloquear um nó do trabalhador, ele fica indisponível para planejamento futuro do pod. Use o **nome** do nó do trabalhador recuperado na etapa anterior.
   ```
   oc cordon <worker_name>
   ```
   {: pre}

3. Verifique se o planejamento do pod está desativado para seu nó do trabalhador.
   ```
   oc get nodes
   ```
   {: pre}
   O nó do trabalhador ficará desativado para planejamento do pod se o status exibir **SchedulingDisabled**.

4. Force os pods para que sejam removidos do nó do trabalhador e reprogramados nos nós do trabalhador restantes no cluster.
  ```
  oc drain <worker_name>
  ```
  {: pre}
  Esse processo pode levar alguns minutos.
5. Reinicialize o nó do trabalhador. Use o ID do trabalhador que é retornado do comando `ibmcloud oc workers --cluster <cluster_name_or_ID>`.
  ```
  ibmcloud oc worker-reboot --cluster <cluster_name_or_ID> --workers <worker_name_or_ID>
  ```
  {: pre}
6. Espere cerca de 5 minutos antes de disponibilizar o seu nó do trabalhador para planejamento de pod para assegurar que a reinicialização esteja concluída. Durante a reinicialização, o estado do nó do trabalhador não muda. A reinicialização de um nó do trabalhador é geralmente concluída em alguns segundos.
7. Disponibilize o nó do trabalhador para planejamento do pod. Use o **nome** para seu nó do trabalhador que é retornado do comando `oc get nodes`.
  ```
  oc uncordon <worker_name>
  ```
  {: pre}

  </br>

```
ibmcloud oc worker-reboot [-f] [--hard] --cluster CLUSTER --worker WORKER [WORKER] [--skip-master-healthcheck] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>-f</code></dt>
<dd>Use essa opção para forçar a reinicialização do nó do trabalhador sem prompts de usuário. Esse valor é opcional.</dd>

<dt><code>--hard</code></dt>
<dd>Use esta opção para forçar uma reinicialização forçada de um nó do trabalhador cortando a energia para o nó do trabalhador. Use essa opção se o nó do trabalhador não estiver responsivo ou o tempo de execução do contêiner do nó do trabalhador não estiver responsivo. Esse valor é opcional.</dd>

<dt><code>--workers <em>WORKER</em></code></dt>
<dd>O nome ou ID de um ou mais nós do trabalhador. Use um espaço para listar múltiplos nós do
trabalhador. Este valor é obrigatório.</dd>

<dt><code>--skip-master-healthcheck </code></dt>
<dd>Ignore uma verificação de funcionamento de seu mestre antes de recarregar ou reinicializar os nós do trabalhador.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-reboot --cluster my_cluster --worker kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>
### `ibmcloud oc worker-reload`
{: #cs_worker_reload}

Recarregue as configurações para um nó do trabalhador.
{: shortdesc}



Um recarregamento poderá ser útil se seu nó do trabalhador tiver problemas, como desempenho lento ou se o nó do trabalhador estiver preso em um estado inoperante. Durante o recarregamento, a máquina do nó do trabalhador é atualizada com a imagem mais recente e os dados são excluídos se não [armazenados fora do nó do trabalhador](/docs/containers?topic=containers-storage_planning#persistent_storage_overview). O endereço IP público e privado do trabalhador do nó permanece o mesmo após a operação de recarregamento.

O recarregamento de um nó do trabalhador aplica atualizações da versão de correção ao nó do trabalhador, mas não atualizações principais ou secundárias. Para ver as mudanças de uma versão de correção para a próxima, revise a documentação de [Log de mudanças da versão](/docs/containers?topic=containers-changelog#changelog).
{: tip}

Antes de recarregar seu nó do trabalhador, certifique-se de que os pods estejam reprogramados em outros nós do trabalhador para ajudar a evitar um tempo de inatividade para seu app ou distorção de dados em seu nó do trabalhador.

1. Liste todos os nós do trabalhador em seu cluster e anote o **nome** do nó do trabalhador que você deseja recarregar.
   ```
   oc get nodes
   ```
   O **nome** retornado nesse comando é o endereço IP privado designado ao nó do trabalhador. É possível localizar mais informações sobre seu nó do trabalhador ao executar o comando `ibmcloud oc workers --cluster <cluster_name_or_ID>` e procurar pelo nó do trabalhador com o mesmo endereço **IP privado**.
2. Marque o nó do trabalhador como não programável em um processo conhecido como bloqueio. Ao bloquear um nó do trabalhador, ele fica indisponível para planejamento futuro do pod. Use o **nome** do nó do trabalhador recuperado na etapa anterior.
   ```
   oc cordon <worker_name>
   ```
   {: pre}

3. Verifique se o planejamento do pod está desativado para seu nó do trabalhador.
   ```
   oc get nodes
   ```
   {: pre}
   O nó do trabalhador ficará desativado para planejamento do pod se o status exibir **SchedulingDisabled**.
 4. Force os pods para que sejam removidos do nó do trabalhador e reprogramados nos nós do trabalhador restantes no cluster.
    ```
    oc drain <worker_name>
    ```
    {: pre}
    Esse processo pode levar alguns minutos.
 5. Recarregue o nó do trabalhador. Use o ID do trabalhador que é retornado do comando `ibmcloud oc workers --cluster <cluster_name_or_ID>`.
    ```
    ibmcloud oc worker-reload --cluster <cluster_name_or_ID> --workers <worker_name_or_ID>
    ```
    {: pre}
 6. Aguarde o recarregamento ser concluído.
 7. Disponibilize o nó do trabalhador para planejamento do pod. Use o **nome** para seu nó do trabalhador que é retornado do comando `oc get nodes`.
    ```
    oc uncordon <worker_name>
    ```
</br>


```
ibmcloud oc worker-reload --cluster CLUSTER --workers WORKER [WORKER] [--skip-master-healthcheck] [-f] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--worker <em>WORKER</em></code></dt>
<dd>O nome ou ID de um ou mais nós do trabalhador. Use um espaço para listar múltiplos nós do
trabalhador. Este valor é obrigatório.</dd>

<dt><code>--skip-master-healthcheck </code></dt>
<dd>Ignore uma verificação de funcionamento de seu mestre antes de recarregar ou reinicializar os nós do trabalhador.</dd>

<dt><code>-f</code></dt>
<dd>Use essa opção para forçar o recarregamento de um nó do trabalhador sem prompts de usuário. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-reload --cluster my_cluster --workers kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>


### `ibmcloud oc worker-rm`
{: #cs_worker_rm}

Remover um ou mais nós do trabalhador de um cluster. Se você remover um nó do trabalhador, o seu cluster se tornará desbalanceado. É possível rebalancear automaticamente seu conjunto de trabalhadores executando o [comando](#cs_rebalance) `ibmcloud oc worker-pool-rebalance`.
{: shortdesc}



Antes de remover o seu nó do trabalhador, certifique-se de que os pods estejam reprogramados em outros nós do trabalhador para ajudar a evitar um tempo de inatividade para o seu app ou a distorção de dados em seu nó do trabalhador.
{: tip}

1. Liste todos os nós do trabalhador em seu cluster e anote o **nome** do nó do trabalhador que você deseja remover.
   ```
   oc get nodes
   ```
   {: pre}
   O **nome** retornado nesse comando é o endereço IP privado designado ao nó do trabalhador. É possível localizar mais informações sobre seu nó do trabalhador ao executar o comando `ibmcloud oc workers --cluster <cluster_name_or_ID>` e procurar pelo nó do trabalhador com o mesmo endereço **IP privado**.
2. Marque o nó do trabalhador como não programável em um processo conhecido como bloqueio. Ao bloquear um nó do trabalhador, ele fica indisponível para planejamento futuro do pod. Use o **nome** do nó do trabalhador recuperado na etapa anterior.
   ```
   oc cordon <worker_name>
   ```
   {: pre}

3. Verifique se o planejamento do pod está desativado para seu nó do trabalhador.
   ```
   oc get nodes
   ```
   {: pre}
   O nó do trabalhador ficará desativado para planejamento do pod se o status exibir **SchedulingDisabled**.
4. Force os pods para que sejam removidos do nó do trabalhador e reprogramados nos nós do trabalhador restantes no cluster.
   ```
   oc drain <worker_name>
   ```
   {: pre}
   Esse processo pode levar alguns minutos.
5. Remova o nó do trabalhador. Use o ID do trabalhador que é retornado do comando `ibmcloud oc workers --cluster <cluster_name_or_ID>`. 
   ```
   ibmcloud oc worker-rm --cluster <cluster_name_or_ID> --worker <worker_name_or_ID>
   ```
   {: pre}
6. Verifique se o nó do trabalhador foi removido.
   ```
   ibmcloud oc workers --cluster <cluster_name_or_ID>
   ```
   {: pre}
</br>

```
ibmcloud oc worker-rm [-f] --cluster CLUSTER --workers WORKER[,WORKER] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>-f</code></dt>
<dd>Use essa opção para forçar a remoção de um nó do trabalhador sem prompts de usuário. Esse valor é opcional.</dd>

<dt><code>--workers <em>WORKER</em></code></dt>
<dd>O nome ou ID de um ou mais nós do trabalhador. Use um espaço para listar múltiplos nós do
trabalhador. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-rm --cluster my_cluster --workers kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>
### `ibmcloud oc worker-update`
{: #cs_worker_update}

Atualize os nós do trabalhador para aplicar as atualizações e correções de segurança mais recentes ao sistema operacional e para atualizar a versão do Kubernetes para corresponder à versão do mestre do Kubernetes. É possível atualizar a versão do Kubernetes mestre com o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_update) `ibmcloud oc cluster-update`. O endereço IP do nó do trabalhador permanece igual após a operação de atualização.
{: shortdesc}



A execução de `ibmcloud oc worker-update` pode causar tempo de inatividade para seus apps e serviços. Durante a atualização, todos os pods são reprogramados em outros nós do trabalhador, o nó do trabalhador tem a imagem reinstalada e os dados são excluídos, se não armazenados fora do pod. Para evitar tempo de inatividade, [assegure-se de que você tenha nós do trabalhador suficientes para manipular a carga de trabalho enquanto os nós do trabalhador selecionados estão atualizando](/docs/containers?topic=containers-update#worker_node).
{: important}

Pode ser necessário mudar seus arquivos YAML para as implementações antes de atualizar. Revise essa [nota sobre a liberação](/docs/containers?topic=containers-cs_versions) para obter detalhes.

```
ibmcloud oc worker-update [-f] --cluster CLUSTER --workers WORKER[,WORKER] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster no qual você lista nós do trabalhador disponíveis. Este valor é obrigatório.</dd>

<dt><code>-f</code></dt>
<dd>Use essa opção para forçar a atualização do mestre sem prompts do usuário. Esse valor é opcional.</dd>

<dt><code>--workers <em>WORKER</em></code></dt>
<dd>O ID de um ou mais nós do trabalhador. Use um espaço para listar múltiplos nós do
trabalhador. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-update --cluster my_cluster --worker kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>
### `ibmcloud oc workers`
{: #cs_workers}

Liste todos os nós do trabalhador em um cluster.
{: shortdesc}



```
ibmcloud oc workers --cluster CLUSTER [--worker-pool POOL] [--show-pools] [--show-deleted] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou o ID do cluster para os nós disponíveis do trabalhador. Este valor é obrigatório.</dd>

<dt><code>--worker-pool <em>POOL</em></code></dt>
<dd>Visualize somente os nós do trabalhador que pertencem ao conjunto de trabalhadores. Para listar os conjuntos de trabalhadores disponíveis, execute `ibmcloud oc worker-pools --cluster <cluster_name_or_ID>`. Esse valor é opcional.</dd>

<dt><code> -- show-pools </code></dt>
<dd>Liste o conjunto de trabalhadores ao qual cada nó do trabalhador pertence. Esse valor é opcional.</dd>

<dt><code>--show-deleted</code></dt>
<dd>Visualize nós do trabalhador que foram excluídos do cluster, incluindo o motivo para a exclusão. Esse valor é opcional.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc workers --cluster my_cluster
```
{: pre}

<br />


## Comandos do conjunto do trabalhador
{: #worker-pool}

Use esse grupo de comandos para visualizar e modificar os conjuntos de trabalhadores para um cluster.
{: shortdesc}

### `ibmcloud oc worker-pool-create`
{: #cs_worker_pool_create}

É possível criar um conjunto de trabalhadores em seu cluster. Quando você incluir um conjunto de trabalhadores, ele não terá uma zona designada por padrão. Você especifica o número de trabalhadores que deseja em cada zona e os tipos para os trabalhadores. O conjunto de trabalhadores recebe as versões padrão do Kubernetes. Para concluir a criação de trabalhadores, [inclua uma zona ou zonas](#cs_zone_add) em seu conjunto.
{: shortdesc}



```
ibmcloud oc worker-pool-create --name POOL_NAME --cluster CLUSTER --machine-type MACHINE_TYPE --size-per-zone WORKERS_PER_ZONE --hardware ISOLATION [--labels LABELS] [--disable-disk-encrypt] [-s] [--json]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--name <em>POOL_NAME</em></code></dt>
<dd>O nome que você deseja dar ao seu conjunto de trabalhadores.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--machine-type <em>MACHINE_TYPE</em></code></dt>
<dd>Escolha um tipo de máquina, ou tipo. É possível implementar os nós do trabalhador como máquinas virtuais em hardware compartilhado ou dedicado ou como máquinas físicas no bare metal. Os tipos de máquinas físicas e virtuais disponíveis variam de acordo com a zona na qual você implementa o cluster. Para obter mais informações, consulte a documentação para o [comando](#cs_machine_types) `ibmcloud oc flavors (macine-types)`. Esse valor é necessário para clusters padrão e não está disponível para clusters livres.</dd>

<dt><code>--size-per-zona <em>WORKERS_PER_ZONE</em></code></dt>
<dd>O número de trabalhadores a serem criados em cada zona. Esse valor é obrigatório e deve ser 1 ou superior.</dd>

<dt><code>--hardware <em>ISOLATION</em></code></dt>
<dd>O nível de isolamento de hardware para seu nó do trabalhador. Use `dedicated` se desejar ter recursos físicos disponíveis que são dedicados apenas a você ou `shared` para permitir que recursos físicos sejam compartilhados com outros clientes IBM. O padrão é `shared`. Para os tipos bare metal, especifique `dedicated`. Este valor é obrigatório.</dd>

<dt><code>--labels <em>LABELS</em></code></dt>
<dd>Os rótulos que você deseja designar aos trabalhadores em seu conjunto. Exemplo: `<key1>=<val1>`,`<key2>=<val2>`</dd>

<dt><code>--disable-disk-encrpyt </code></dt>
<dd>Especifica que o disco não está criptografado. O valor padrão é <code>false</code>.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-pool-create --name my_pool --cluster my_cluster --machine-type b3c.4x16 --size-per-zone 6
```
{: pre}

</br>


### `ibmcloud oc worker-pool-get`
{: #cs_worker_pool_get}

Visualize os detalhes de um conjunto de trabalhadores.
{: shortdesc}



```
ibmcloud oc worker-pool-get --worker-pool WORKER_POOL --cluster CLUSTER [-s] [--json]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>-- worker-conjunto <em>WORKER_POOL</em></code></dt>
<dd>O nome do conjunto de nós do trabalhador do qual você deseja visualizar os detalhes. Para listar os conjuntos de trabalhadores disponíveis, execute `ibmcloud oc worker-pools --cluster <cluster_name_or_ID>`. Este valor é obrigatório.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster no qual o conjunto de trabalhadores está localizado. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-pool-get --worker-pool pool1 --cluster my_cluster
```
{: pre}

**Saída de exemplo**:

  ```
  Name:               pool
  ID:                 a1a11b2222222bb3c33c3d4d44d555e5-f6f777g
  State:              active
  Hardware:           shared
  Zones:              dal10,dal12
  Workers per zone:   3
  Machine type:       b3c.4x16.encrypted
  Labels:             -
  Version:            1.13.8_1512
  ```
  {: screen}

</br>
### `ibmcloud oc worker-pool-rebalance`
{: #cs_rebalance}

Rebalancear um conjunto de trabalhadores em um cluster depois de excluir um nó do trabalhador. Quando você executa esse comando, um novo trabalhador ou trabalhadores são incluídos no conjunto de trabalhadores para que o conjunto de trabalhadores tenha o mesmo número de nós por zona que você especificou.
{: shortdesc}



```
ibmcloud oc worker-pool-rebalance --cluster CLUSTER --worker-pool WORKER_POOL [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code><em>--cluster CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code><em>--worker-pool WORKER_POOL</em></code></dt>
<dd>O conjunto de trabalhadores que você deseja rebalancear. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-pool-rebalance --cluster my_cluster --worker-pool my_pool
```
{: pre}

</br>
### `ibmcloud oc worker-pool-resize`
{: #cs_worker_pool_resize}

Redimensione seu conjunto de trabalhadores para aumentar ou diminuir o número de nós do trabalhador que estão em cada zona de seu cluster. Seu conjunto do trabalhador deve ter pelo menos um nó do trabalhador.
{: shortdesc}



```
ibmcloud oc worker-pool-resize --worker-pool WORKER_POOL --cluster CLUSTER --size-per-zone WORKERS_PER_ZONE [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>-- worker-conjunto <em>WORKER_POOL</em></code></dt>
<dd>O nome do conjunto de nós do trabalhador que se deseja atualizar. Este valor é obrigatório.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster para o qual você deseja redimensionar conjuntos de trabalhadores. Este valor é obrigatório.</dd>

<dt><code>--size-per-zona <em>WORKERS_PER_ZONE</em></code></dt>
<dd>O número de trabalhadores que você deseja ter em cada zona. Esse valor é obrigatório e deve ser 1 ou superior.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>

</dl>

**Exemplo**:
```
ibmcloud oc worker-pool-resize --cluster my_cluster --worker-pool my_pool --size-per-zone 3
```
{: pre}

</br>
### `ibmcloud oc worker-pool-rm`
{: #cs_worker_pool_rm}

Remover um conjunto de trabalhadores do seu cluster. Todos os nós do trabalhador no conjunto são excluídos. Seus pods são reprogramados quando você exclui. Para evitar tempo de inatividade, certifique-se de que você tenha trabalhadores suficientes para executar a carga de trabalho.
{: shortdesc}



```
ibmcloud oc worker-pool-rm --worker-pool WORKER_POOL --cluster CLUSTER [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>-- worker-conjunto <em>WORKER_POOL</em></code></dt>
<dd>O nome do conjunto de nós do trabalhador que você deseja remover. Este valor é obrigatório.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster do qual você deseja remover o conjunto de trabalhadores. Este valor é obrigatório.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-pool-rm --cluster my_cluster --worker-pool pool1
```
{: pre}

</br>
### `ibmcloud oc worker-pools`
{: #cs_worker_pools}

Liste todos os conjuntos de trabalhadores em um cluster.
{: shortdesc}



```
ibmcloud oc worker-pools --cluster CLUSTER [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Visualizador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>-- cluster <em>CLUSTER_NAME_OR_ID</em></code></dt>
<dd>O nome ou ID do cluster para o qual você deseja listar os conjuntos de trabalhadores. Este valor é obrigatório.</dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc worker-pools --cluster my_cluster
```
{: pre}

</br>
### `ibmcloud oc zone-add`
{: #cs_zone_add}

Depois de criar um cluster ou um conjunto de trabalhadores, é possível incluir uma zona. Quando você incluir uma zona, os nós do trabalhador serão incluídos na nova zona para corresponder ao número de trabalhadores por zona que você especificou para o conjunto de trabalhadores. É possível incluir mais de uma zona apenas se o seu cluster está em uma área metropolitana multizona.
{: shortdesc}



```
ibmcloud oc zone-add --zone ZONE --cluster CLUSTER --worker-pools WORKER_POOL1[,WORKER_POOL2] --private-vlan PRIVATE_VLAN [--public-vlan PUBLIC_VLAN] [--private-only] [--json] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>A zona que você deseja incluir. Ele deve ser uma [zona com capacidade para múltiplas zonas](/docs/containers?topic=containers-regions-and-zones#zones) dentro da região do cluster. Este valor é obrigatório.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--worker-pool <em>WORKER_POOLS</em></code></dt>
<dd>Uma lista separada por vírgulas de conjuntos de trabalhadores aos quais a zona é incluída. Pelo menos um conjunto de trabalhadores é necessário.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd><p>O ID da VLAN privada. Esse valor é condicional.</p>
    <p>Se você tiver uma VLAN privada na zona, esse valor deverá corresponder ao ID de VLAN privada de um ou mais nós do trabalhador no cluster. Para ver as VLANs que estão disponíveis para você, execute <code>ibmcloud oc cluster-get --cluster &lt;cluster&gt; --showResources</code>. Novos nós do trabalhador são incluídos na VLAN especificada, mas as VLANs de quaisquer nós do trabalhador existentes não mudam.</p>
    <p>Se você não tiver uma VLAN privada ou pública nessa zona, não especifique essa opção. Uma VLAN privada e pública é automaticamente criada para você quando você inclui inicialmente uma zona para o seu conjunto de trabalhadores.</p>
    <p>Se você tiver múltiplas VLANs para um cluster, múltiplas sub-redes na mesma VLAN ou em um cluster multizona, você deverá ativar um [Virtual Router Function (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) para sua conta de infraestrutura do IBM Cloud para que os nós do trabalhador possam se comunicar entre si na rede privada. Para ativar o VRF, [entre em contato com o seu representante de conta de infraestrutura do IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Para verificar se um VRF já está ativado, use o comando `ibmcloud account show`. Se não for possível ou você não desejar ativar o VRF, ative o [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Para executar essa ação, você precisa da [permissão de infraestrutura](/docs/containers?topic=containers-users#infra_access) **Rede > Gerenciar a rede VLAN Spanning** ou é possível solicitar ao proprietário da conta para ativá-la. Para verificar se a ampliação da VLAN já está ativada, use o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud oc vlan-spanning-get --region <region>`.</p></dd>

<dt><code>--public-vlan <em>PUBLIC_VLAN</em></code></dt>
<dd><p>O ID da VLAN pública. Esse valor será necessário se você desejar expor as cargas de trabalho nos nós para o público depois de criar o cluster. Ele deve corresponder ao ID da VLAN pública de um ou mais nós do trabalhador no cluster para a zona. Para ver as VLANs que estão disponíveis para você, execute <code>ibmcloud oc cluster-get --cluster &lt;cluster&gt; --showResources</code>. Novos nós do trabalhador são incluídos na VLAN especificada, mas as VLANs de quaisquer nós do trabalhador existentes não mudam.</p>
    <p>Se você não tiver uma VLAN privada ou pública nessa zona, não especifique essa opção. Uma VLAN privada e pública é automaticamente criada para você quando você inclui inicialmente uma zona para o seu conjunto de trabalhadores.</p>
    <p>Se você tiver múltiplas VLANs para um cluster, múltiplas sub-redes na mesma VLAN ou em um cluster multizona, você deverá ativar um [Virtual Router Function (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) para sua conta de infraestrutura do IBM Cloud para que os nós do trabalhador possam se comunicar entre si na rede privada. Para ativar o VRF, [entre em contato com o seu representante de conta de infraestrutura do IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Para verificar se um VRF já está ativado, use o comando `ibmcloud account show`. Se não for possível ou você não desejar ativar o VRF, ative o [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Para executar essa ação, você precisa da [permissão de infraestrutura](/docs/containers?topic=containers-users#infra_access) **Rede > Gerenciar a rede VLAN Spanning** ou é possível solicitar ao proprietário da conta para ativá-la. Para verificar se a ampliação da VLAN já está ativada, use o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud oc vlan-spanning-get --region <region>`.</p></dd>

<dt><code>-- somente privado </code></dt>
<dd>Use essa opção para evitar que uma VLAN pública seja criada. Necessário somente quando você especifica a sinalização `--private-vlan` e não inclui a sinalização `--public-vlan`.<p class="note">Se os nós do trabalhador estão configurados somente com uma VLAN privada, deve-se ativar o terminal em serviço privado ou configurar um dispositivo de gateway. Para obter mais informações, consulte [Planejando a configuração do cluster privado e do nó do trabalhador](/docs/containers?topic=containers-plan_clusters#private_clusters).</p></dd>

<dt><code>--json</code></dt>
<dd>Imprime a saída de comando no formato JSON. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc zone-add --zone dal10 --cluster my_cluster --worker-pools pool1,pool2,pool3 --private-vlan 2294021
```
{: pre}

</br>


### `ibmcloud oc zone-network-set`
{: #cs_zone_network_set}

**Somente clusters de múltiplas zonas**: configure os metadados de rede para um conjunto de trabalhadores para usar uma VLAN pública ou privada diferente para a zona do que foi usada anteriormente. Os nós do trabalhador que já foram criados no conjunto continuam a usar a VLAN pública ou privada anterior, mas os novos nós do trabalhador no conjunto usam os novos dados de rede.
{: shortdesc}



```
ibmcloud oc zone-network-set --zone ZONE --cluster CLUSTER --worker-pools WORKER_POOL1[,WORKER_POOL2] --private-vlan PRIVATE_VLAN [--public-vlan PUBLIC_VLAN] [--private-only] [-f] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>A zona que você deseja incluir. Ele deve ser uma [zona com capacidade para múltiplas zonas](/docs/containers?topic=containers-regions-and-zones#zones) dentro da região do cluster. Este valor é obrigatório.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>--worker-pool <em>WORKER_POOLS</em></code></dt>
<dd>Uma lista separada por vírgulas de conjuntos de trabalhadores aos quais a zona é incluída. Pelo menos um conjunto de trabalhadores é necessário.</dd>

<dt><code>--private-vlan <em>PRIVATE_VLAN</em></code></dt>
<dd>O ID da VLAN privada. Esse valor é necessário, se você deseja usar a mesma VLAN privada ou uma diferente daquela que usou para seus outros nós do trabalhador. Novos nós do trabalhador são incluídos na VLAN especificada, mas as VLANs de quaisquer nós do trabalhador existentes não mudam.<p class="note">As VLANs privadas e públicas devem ser compatíveis e podem ser determinadas por meio do prefixo de ID do **Roteador**.</p></dd>

<dt><code>--public-vlan <em>PUBLIC_VLAN</em></code></dt>
<dd>O ID da VLAN pública. Esse valor será necessário somente se você desejar mudar a VLAN pública para a zona. Para mudar a VLAN pública, deve-se sempre fornecer uma VLAN privada compatível. Novos nós do trabalhador são incluídos na VLAN especificada, mas as VLANs de quaisquer nós do trabalhador existentes não mudam.<p class="note">As VLANs privadas e públicas devem ser compatíveis e podem ser determinadas por meio do prefixo de ID do **Roteador**.</p></dd>

<dt><code>-- somente privado </code></dt>
<dd>Opcional: desconfigure a VLAN pública para que os trabalhadores nessa zona sejam conectados a somente uma VLAN privada.</dd>

<dt><code>-f</code></dt>
<dd>Force o comando a ser executado sem prompts do usuário. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Uso**:
<ol><li>Verifique as VLANs que estão disponíveis em seu cluster. <pre class="pre"><code>ibmcloud oc cluster get --cluster &lt;cluster_name_or_ID&gt; --showResources</code></pre><p>Saída de exemplo:</p>
<pre class="screen"><code>Subnet VLANs
VLAN ID   Subnet CIDR         Public   User-managed
229xxxx   169.xx.xxx.xxx/29   true     false
229xxxx   10.xxx.xx.x/29      false    false</code></pre></li>
<li>Verifique se os IDs de VLAN pública e privada que você deseja usar são compatíveis. Para serem compatíveis, o <strong>Roteador</strong> deve ter o mesmo ID de pod. Os roteadores de VLAN privada sempre iniciam com <code>bcr</code> (roteador de backend) e roteadores de VLAN pública sempre iniciam com <code>fcr</code> (roteador de front-end). Ao criar um cluster e especificar as VLANs públicas e privadas, a combinação de número e letra após esses prefixos devem corresponder.<pre class="pre"><code>ibmcloud oc vlans --zone &lt;zone&gt;</code></pre><p>Saída de exemplo:</p>
<pre class="screen"><code>ID        Name   Number   Type      Router         Supports Virtual Workers
229xxxx          1234     private   bcr01a.dal12   true
229xxxx          5678     public    fcr01a.dal12   true</code></pre><p>Observe que os IDs de pod de <strong>Roteador</strong> correspondem: `01a` e `01a`. Se um ID de pod fosse `01a` e o outro fosse `02a`, não seria possível configurar esses IDs de VLAN pública e privada para o conjunto de trabalhadores.</p></li>
<li>Se você não tiver nenhuma VLAN disponível, será possível <a href="/docs/infrastructure/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans">solicitar novas VLANs</a>.</li></ol>

**Exemplo**:
```
ibmcloud oc zone-network-set --zone dal10 --cluster my_cluster --worker-pools pool1,pool2,pool3 --private-vlan 2294021
```
{: pre}

</br>
### `ibmcloud oc zone-rm`
{: #cs_zone_rm}

**Somente clusters de múltiplas zonas**: remova uma zona de todos os conjuntos de trabalhadores em seu cluster. Todos os nós do trabalhador no conjunto de trabalhadores para essa zona são excluídos.
{: shortdesc}



Antes de remover uma zona, assegure-se de ter nós de trabalhadores suficientes em outras zonas no cluster para que seus pods possam reprogramar. O reescalonamento de seus pods pode evitar um tempo de inatividade para seu aplicativo ou distorção de dados em seu nó do trabalhador.
{: tip}

```
ibmcloud oc zone-rm --zone ZONE --cluster CLUSTER [-f] [-s]
```
{: pre}

**Permissões mínimas necessárias**: a função da plataforma **Operador** para o cluster no {{site.data.keyword.containerlong_notm}}

**Opções de comando**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>A zona que você deseja remover. Este valor é obrigatório.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>O nome ou ID do cluster. Este valor é obrigatório.</dd>

<dt><code>-f</code></dt>
<dd>Forçar a atualização sem prompts do usuário. Esse valor é opcional.</dd>

<dt><code>-s</code></dt>
<dd>Não mostrar a mensagem do dia ou os lembretes de atualização. Esse valor é opcional.</dd>
</dl>

**Exemplo**:
```
ibmcloud oc zone-rm --zone dal10 --cluster my_cluster
```
{: pre}


