---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, mzr, szr, multizone, multi az

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


# Localidades
{: #regions-and-zones}

É possível implementar clusters do {{site.data.keyword.openshiftlong}} em todo o mundo. Ao criar um cluster, seus recursos permanecem no local no qual você implementa o cluster. Para trabalhar com seu cluster, é possível acessar o OpenShift Service por meio de um terminal de API global.
{:shortdesc}

![Localizações do Red Hat OpenShift on IBM Cloud](images/locations-roks.png)

_Localizações do Red Hat OpenShift on IBM Cloud_


## Localizações do Red Hat OpenShift on IBM Cloud
{: #locations}

Os recursos do {{site.data.keyword.cloud_notm}} são organizados em uma hierarquia de locais geográficos. O Red Hat OpenShift on IBM Cloud está disponível em uma sub-rede dessas localizações, incluindo todas as seis regiões com capacidade para várias zonas mundiais. Outros serviços {{site.data.keyword.cloud_notm}} podem estar disponíveis globalmente ou em um local específico.
{: shortdesc}

### Locais disponíveis
{: #available-locations}

Para listar localizações disponíveis do Red Hat OpenShift on IBM Cloud, use o comando `ibmcloud oc supported-locations`.
{: shortdesc}

A imagem a seguir é usada como um exemplo para explicar como as localizações do Red Hat OpenShift on IBM Cloud são organizadas.

![Organização de localizações do Red Hat OpenShift on IBM Cloud](images/cs_regions_hierarchy.png)

<table summary="A tabela mostra a organização de localizações do Red Hat OpenShift on IBM Cloud. As linhas devem ser lidas da esquerda para a direita, com o tipo de localização na coluna um, um exemplo do tipo na coluna dois e a descrição na coluna três.">
<caption>Organização de localizações do Red Hat OpenShift on IBM Cloud.</caption>
  <thead>
  <th>Tipo</th>
  <th>Exemplo</th>
  <th>Descrição</th>
  </thead>
  <tbody>
    <tr>
      <td>Geografia</td>
      <td>América do Norte (`na`)</td>
      <td>Um agrupamento organizacional que é baseado em continentes geográficos.</td>
    </tr>
    <tr>
      <td>Country</td>
      <td>Canadá (`ca`)</td>
      <td>O país do local dentro da geografia.</td>
    </tr>
    <tr>
      <td>Metro</td>
      <td>Cidade do México (`mex-cty`), Dallas (`dal`)</td>
      <td>O nome de uma cidade em que 1 ou mais data centers (zonas) estão localizados. Uma área metropolitana pode ter capacidade de multizona e ter data centers com capacidade de multizona, como Dallas, ou pode ter somente data centers de zona única, como a Cidade do México. Se você criar um cluster em uma área metropolitana com capacidade de multizona, o principal do Kubernetes e os nós do trabalhador poderão ser difundidos entre as zonas para alta disponibilidade.</td>
    </tr>
    <tr>
      <td>Data center (zona)</td>
      <td>Dallas 12 (`dal12`)</td>
      <td>Um local físico da infraestrutura de cálculo, de rede e de armazenamento e do resfriamento e energia relacionados que hospedam os serviços e aplicativos de nuvem. Os clusters podem ser distribuídos entre data centers ou zonas em uma arquitetura de multizona para alta disponibilidade. As zonas são isoladas umas das outras, o que assegura nenhum ponto único de falha compartilhado.</td>
    </tr>
  </tbody>
  </table>

### Localizações de várias zonas no Red Hat OpenShift on IBM Cloud
{: #zones}

As tabelas a seguir listam as localizações de várias zonas disponíveis no Red Hat OpenShift on IBM Cloud. É possível escolher criar clusters com nós do trabalhador em uma zona da metrópole de várias zonas ou difundir os trabalhadores entre todas as três zonas dentro de cada metrópole para proteger seus apps de uma falha de zona. Se você criar os trabalhadores em uma única zona ou entre zonas, as réplicas do seu mestre altamente disponível serão automaticamente difundidas entre as zonas.
{: shortdesc}

Para determinar rapidamente se uma zona tem capacidade de várias zonas, é possível executar `ibmcloud oc supported-locations` e procurar o valor na coluna `Multizone Metro`.
{: tip}

**Locais de área metropolitana de multizona**

<table summary="A tabela mostra as localizações metropolitanas de várias zonas disponíveis no Red Hat OpenShift on IBM Cloud. As linhas devem ser lidas da esquerda para a direita. A coluna um é a geografia em que a localização está; a coluna dois é o país da localização; a coluna três é a metrópole da localização; a coluna quatro é o data center e a coluna cinco é a região descontinuada na qual a localização costumava ser organizada.">
<caption>Localizações metropolitanas de várias zonas disponíveis no Red Hat OpenShift on IBM Cloud.</caption>
  <thead>
  <th>Geografia</th>
  <th>Country</th>
  <th>Metro</th>
  <th>Datacenter</th>
  <th>Região descontinuada</th>
  </thead>
  <tbody>
    <tr>
      <td>Ásia-Pacífico</td>
      <td>Australia</td>
      <td>Sydney</td>
      <td>syd01, syd04, syd05</td>
      <td>Sul da Ásia-Pacífico (`ap-south`, `au-syd`)</td>
    </tr>
    <tr>
      <td>Ásia-Pacífico</td>
      <td>Japão</td>
      <td>Tóquio</td>
      <td>tok02, tok04, tok05</td>
      <td>Norte da Ásia-Pacífico (`ap-north`, `jp-tok`)</td>
    </tr>
    <tr>
      <td>Europa</td>
      <td>Alemanha</td>
      <td>Frankfurt</td>
      <td>fra02, fra04, fra05</td>
      <td>UE Central (`eu-central`, `eu-de`)</td>
    </tr>
    <tr>
      <td>Europa</td>
      <td>United Kingdom</td>
      <td>Londres</td>
      <td>lon04, lon05, lon06</td>
      <td>Sul do Reino Unido (`uk-south`, `eu-gb`)</td>
    </tr>
    <tr>
      <td>América do Norte</td>
      <td>Estados Unidos</td>
      <td>Dallas</td>
      <td>dal10, dal12, dal13</td>
      <td>Sul dos EUA (`us-south`)</td>
    </tr>
    <tr>
      <td>América do Norte</td>
      <td>Estados Unidos</td>
      <td>Washington, D.C.</td>
      <td>wdc04, wdc06, wdc07</td>
      <td>Leste dos EUA (`us-east`)</td>
    </tr>
  </tbody>
  </table>

### Clusters de múltiplas zonas
{: #regions_multizone}

Em um cluster de multizona, os recursos de seu cluster são difundidos entre múltiplas zonas para maior disponibilidade.
{: shortdesc}

1.  Os nós do trabalhador são distribuídos em múltiplas zonas no local de área metropolitana para fornecer mais disponibilidade para seu cluster. As réplicas do principal do Kubernetes também são difundidas entre as zonas. Ao iniciar ações de orquestração do contêiner local, como comandos `oc`, as informações são trocadas entre seu mestre e os nós do trabalhador por meio do terminal global.

2.  Outros recursos de cluster, como armazenamento, rede, cálculo ou apps em execução em pods, variam em como são implementados nas zonas em seu cluster de múltiplas zonas. Para obter mais informações, revise estes tópicos:
    *   Configurando o [armazenamento de arquivo](/docs/openshift?topic=openshift-file_storage#add_file) e o [armazenamento de bloco](/docs/openshift?topic=openshift-block_storage#add_block) em clusters de multizona ou [escolhendo uma solução de armazenamento persistente de multizona](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).
    *   [Ativando o acesso público ou privado a um app usando um serviço de balanceador de carga de rede (NLB) em um cluster de multizona](/docs/containers?topic=containers-loadbalancer#multi_zone_config).
    *   [Gerenciando o tráfego de rede usando o Ingress](/docs/containers?topic=containers-ingress-about).
    *   [Aumentando a disponibilidade de seu app](/docs/containers?topic=containers-app#increase_availability).

3.  Ao iniciar ações de gerenciamento de cluster, como usar [comandos `ibmcloud oc`](/docs/openshift?topic=openshift-kubernetes-service-cli), informações básicas sobre o cluster (como nome, ID, usuário, comando) são roteadas por meio do terminal global.

<br />


## Acessando o terminal global
{: #endpoint}

É possível organizar seus recursos em serviços do {{site.data.keyword.cloud_notm}} usando locais do {{site.data.keyword.cloud_notm}} (anteriormente chamados de regiões). Por exemplo, é possível criar um cluster do OpenShift usando uma imagem do Docker privada armazenada em seu {{site.data.keyword.registryshort_notm}} do mesmo local. Para acessar esses recursos, é possível usar os terminais globais e filtrar por local.
{:shortdesc}

### Efetuando login no {{site.data.keyword.cloud_notm}}
{: #login-ic}

Quando você efetua login na linha de comandos do {{site.data.keyword.cloud_notm}} (`ibmcloud`), é solicitado que selecione uma região. Entretanto, essa região não afeta o terminal do plug-in do Red Hat OpenShift on IBM Cloud (`ibmcloud oc`), que ainda usa o terminal global. Observe que ainda é necessário ter como destino o grupo de recursos em que seu cluster está, caso ele não esteja no grupo de recursos padrão.
{: shortdesc}

Para efetuar login no terminal de API global do {{site.data.keyword.cloud_notm}} e ter como destino o grupo de recursos em que seu cluster está:
```
ibmcloud login -a https://cloud.ibm.com -g <nondefault_resource_group_name>
```
{: pre}

### Efetuando login no Red Hat OpenShift on IBM Cloud
{: #login-iks}

Quando você efetua login no {{site.data.keyword.cloud_notm}}, é possível acessar o {{site.data.keyword.containershort_notm}}. Para ajudar a iniciar, confira os recursos a seguir para usar a CLI e a API do Red Hat OpenShift on IBM Cloud.
{: shortdesc}

**CLI do Red Hat OpenShift on IBM Cloud**:

[Configure sua CLI para usar o plug-in `ibmcloud oc`](/docs/openshift?topic=openshift-openshift-cli). Por padrão, você efetua login no terminal global do Red Hat OpenShift on IBM Cloud, `https://containers.cloud.ibm.com`.

Quando você usar a nova funcionalidade global na CLI do Red Hat OpenShift on IBM Cloud, considere as mudanças a seguir por meio da funcionalidade baseada em região anterior.

* Listando recursos:
  * Ao listar os recursos, assim como com os comandos `ibmcloud oc clusters`, `ibmcloud oc subnets` ou `ibmcloud oc zones`, os recursos em todas as localizações são retornados. Para filtrar recursos por um local específico, determinados comandos incluem uma sinalização `--locations`. Por exemplo, se você filtrar clusters para a metrópole `wdc`, clusters de várias zonas nessa metrópole e clusters de zona única nos data centers (zonas) dentro dessa metrópole serão retornados. Se você filtrar clusters para o data center (zona) `wdc06`, clusters de várias zonas que tiverem um nó do trabalhador nessa zona e clusters de zona única nessa zona serão retornados. Observe que é possível passar um local ou uma lista de locais separada por vírgula.
    Exemplo para filtrar por local:
    ```
    ibmcloud oc clusters --locations dal
    ```
    {: pre}
  * Outros comandos não retornam recursos em todos os locais. Para executar os comandos `credential-set/unset/get`, `api-key-reset` e `vlan-spanning-get`, deve-se especificar uma região em `--region`.

* Trabalhando com recursos:
  * Ao usar o terminal global, será possível trabalhar com recursos aos quais você tem permissões de acesso em qualquer localização, mesmo se você configurar uma região executando `ibmcloud oc region-set` e o recurso com o qual deseja trabalhar estiver em outra região.
  * Se você tiver clusters com o mesmo nome em diferentes regiões, será possível usar o ID do cluster quando executar comandos ou configurar uma região com o comando `ibmcloud oc region-set` e usar o nome do cluster quando executar comandos.

* Funcionalidade anterior:
  * Se você precisar listar e trabalhar com recursos de uma região apenas, será possível usar o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_init) `ibmcloud oc init` para ter como destino um terminal regional em vez do terminal global.
    Exemplo para que o terminal regional do Sul dos EUA seja o destino:
    ```
    ibmcloud oc init --host https://us-south.containers.cloud.ibm.com
    ```
    {: pre}
  * Para usar a funcionalidade global, é possível usar o comando `ibmcloud oc init` novamente para ter o terminal global como destino. Exemplo para destinar o terminal global novamente:
    ```
    ibmcloud oc init --host https://containers.cloud.ibm.com
    ```
    {: pre}

</br></br>
**API do Red Hat OpenShift on IBM Cloud**:
* [Introdução à API](/docs/containers?topic=containers-cs_cli_install#cs_api).
* [Visualizar documentação sobre os comandos da API](https://containers.cloud.ibm.com/global/swagger-global-api/).
* Gere um cliente da API para usar na automação usando a [API `swagger.json`](https://containers.cloud.ibm.com/global/swagger-global-api/swagger.json).

Para interagir com a API global do Red Hat OpenShift on IBM Cloud, insira o tipo de comando e anexe `global/v1/command` ao terminal.

Exemplo da API global `GET /clusters`:
```
GET https://containers.cloud.ibm.com/global/v1/clusters
```
{: codeblock}

</br>

Se for necessário especificar uma região em uma chamada da API, remova o parâmetro `/global` do caminho e passe o nome da região no cabeçalho `X-Region`. Para listar as regiões disponíveis, execute `ibmcloud oc regions`.

<br />

