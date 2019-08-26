---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, version, rhel

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

# Informações de Versão e ações de atualização
{: #openshift_versions}

Os clusters do {{site.data.keyword.openshiftlong}} são executados no OpenShift versão 3.11, que inclui o projeto Kubernetes versão 1.11. O sistema operacional do nó do trabalhador é o Red Hat Enterprise Linux 7.
{: shortdesc}

Para obter mais informações sobre as versões do projeto OpenShift e do Kubernetes, revise as informações a seguir.
* [Visão geral de notas sobre a liberação do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/release_notes/index.html)
* [Log de mudanças do Kubernetes ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md)

## Tipos de atualização
{: #openshift_update_types}

Seu cluster do Red Hat OpenShift on IBM Cloud tem três tipos de atualizações: principal, secundária e correção. Conforme as atualizações se tornam disponíveis, você é notificado ao visualizar informações sobre os nós do trabalhador, como no console ou na CLI com os comandos `ibmcloud oc workers --cluster <cluster>` ou `ibmcloud oc worker-get --cluster <cluster> --worker <worker>`.
{:shortdesc}

|Tipo de atualização|Exemplos de rótulos de versão|Atualizado por|Impacto
|-----|-----|-----|-----|
|Principal|3.x.x|Você|Mudanças de operação para clusters, incluindo scripts ou implementações.|
|Menor|x.11.x|Você|Mudanças de operação para clusters, incluindo scripts ou implementações.|
|Correção|x.x.104_1507|IBM e você|Correções do OpenShift, bem como outras atualizações de componente do {{site.data.keyword.cloud_notm}} Provider, como correções de segurança e do sistema operacional. A IBM atualiza os mestres automaticamente, mas você aplica correções a nós do trabalhador. Veja mais sobre correções na seção a seguir.|
{: caption="Impactos das atualizações do OpenShift" caption-side="top"}

<dl>
  <dt>**Atualizações principais e secundárias (3.11)**</dt>
  <dd><p>Primeiro, [atualize seu nó principal](/docs/openshift?topic=containers-update#master) e, em seguida, [atualize os nós do trabalhador](/docs/openshift?topic=containers-update#worker_node). Os nós do trabalhador não podem executar uma versão principal ou secundária do OpenShift que é maior que os mestres.</p><p class="note">Se você usar uma versão da CLI `oc` ou `kubectl` que corresponda pelo menos à versão `major.minor` de seus clusters, talvez obtenha resultados inesperados. Assegure-se de manter seu cluster e [versões da CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) atualizadas.</p></dd>
  <dt>**Atualizações de correção (x.x.104_1507)**</dt>
  <dd><p>As correções principais são aplicadas automaticamente, mas você inicia as atualizações de correções do nó do trabalhador. Os nós do trabalhador também podem executar versões de correção que são maiores que as principais. Conforme as atualizações se tornam disponíveis, você é notificado ao visualizar informações sobre os nós principais e do trabalhador no console ou CLI do {{site.data.keyword.cloud_notm}}, assim como com os comandos a seguir: `ibmcloud oc clusters`, `cluster-get`, `workers` ou `worker-get`.</p>
  <p>As correções podem ser para nós do trabalhador, mestres ou ambos.</p>
  <ul><li>**Correções do nó do trabalhador**: verifique mensalmente para ver se uma atualização está disponível e use o [comando](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_update) `ibmcloud oc worker-update` ou o [comando](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) `ibmcloud oc worker-reload` para aplicar essas correções de segurança e do sistema operacional. Durante uma atualização ou um recarregamento, a imagem da máquina do nó do trabalhador será recriada e os dados serão excluídos se não [armazenados fora do nó do trabalhador](/docs/openshift?topic=containers-storage_planning#persistent_storage_overview).</li>
  <li>**Correções de mestre**: as correções de mestre são aplicadas automaticamente ao longo do curso de vários dias, portanto, uma versão de correção de mestre pode aparecer como disponível antes de ser aplicada ao seu mestre. A automação de atualização também ignora clusters que estão em um estado não funcional ou têm operações atualmente em andamento. Ocasionalmente, a IBM pode desativar as atualizações automáticas para um fix pack de mestre específico, conforme observado no log de mudanças, como uma correção que será necessária somente se um mestre for atualizado de uma versão secundária para outra. Em qualquer um desses casos, é possível escolher usar com segurança o [comando](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_update) `ibmcloud oc cluster-update` sem esperar que a automação de atualização se aplique.</li></ul></dd>
</dl>

<br />


## Histórico de liberação
{: #openshift_release_history}

A tabela a seguir registra o histórico de liberação de versão do Red Hat OpenShift on IBM Cloud. É possível usar essas informações para propósitos de planejamento, como para estimar os períodos de tempo gerais quando uma determinada liberação pode se tornar não suportada. Após a comunidade do Red Hat OpenShift liberar uma atualização de versão, a equipe da IBM inicia um processo de reforço e teste da liberação para ambientes do {{site.data.keyword.containerlong_notm}}. As datas de liberação disponíveis e não suportadas dependem dos resultados desses testes, das atualizações de comunidade, das correções de segurança e das mudanças de tecnologia entre as versões. Planeje manter a versão do cluster mestre e do nó do trabalhador atualizada.
{: shortdesc}

O Red Hat OpenShift on IBM Cloud foi fornecido em disponibilidade geral primeiro com o OpenShift versão 3.11, que inclui o projeto Kubernetes versão 1.11. As datas marcadas com o símbolo (`†`) são tentativas e estão sujeitas a mudança.
{: important}

<table summary="Esta tabela mostra o histórico de liberação para o Red Hat OpenShift on IBM Cloud.">
<caption>Histórico de liberação do Red Hat OpenShift on IBM Cloud.</caption>
<col width="20%" align="center">
<col width="20%">
<col width="30%">
<col width="30%">
<thead>
<tr>
<th>Suportado?</th>
<th>Versão do OpenShift/Kubernetes</th>
<th>Red Hat OpenShift on IBM Cloud<br>data de liberação</th>
<th>Red Hat OpenShift on IBM Cloud<br>data não suportada</th>
</tr>
</thead>
<tbody>
<tr>
  <td><img src="images/checkmark-filled.png" align="left" width="32" style="width:32px;" alt="This version is supported."/></td>
  <td>3.11/1.11</td>
  <td>1º de agosto de 2019 à 0h UTC</td>
  <td>`†`</td>
</tr>
</tbody>
</table>
