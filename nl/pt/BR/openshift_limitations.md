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
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Limitações de serviço
{: #openshift_limitations}

Revise as limitações a seguir para o {{site.data.keyword.openshiftlong}}. Para limitações gerais do produto, como chamadas de API ou número de pods por nó do trabalhador, consulte as [limitações de serviço do {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-ibm-cloud-kubernetes-service-technology#tech_limits).
{: shortdesc}

## Grupo
{: #oc_limits_cluster}

*   É possível criar somente clusters padrão, não clusters grátis. Em vez disso, é possível criar um cluster Kubernetes grátis e, em seguida, reimplementar os apps que você testar no cluster Kubernetes para seu cluster do OpenShift.
*   [Localizações](/docs/openshift?topic=openshift-regions-and-zones) estão disponíveis em todas as seis áreas metropolitanas de várias zonas do mundo: Dallas, Frankfurt, Londres, Sydney, Tóquio e Washington DC.
*   Não é possível criar um cluster com nós do trabalhador que executam múltiplos sistemas operacionais, como o OpenShift no Red Hat Enterprise Linux e o Kubernetes da comunidade no Ubuntu.

## Storage
{: #oc_limits_storage}

O armazenamento de objeto de arquivo, de bloco e de nuvem do {{site.data.keyword.cloud_notm}} é suportado. O software-defined storage (SDS) do Portworx não é suportado.

Devido à maneira como o armazenamento de arquivo NFS do {{site.data.keyword.cloud_notm}} configura as permissões de usuário do Linux, você pode encontrar erros ao usar o armazenamento de arquivo. Em caso positivo, pode ser necessário configurar [restrições de contexto de segurança do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html) ou usar um tipo de armazenamento diferente.

## Métricas 
{: #oc_limits_metrics}

O gerenciador de alerta [Prometheus integrado](/docs/openshift?topic=openshift-openshift_apps#openshift_access_oc_services) inclui duas regras que são exibidas como alertas ativos em um estado `FIRING`: `KubeControllerManagerDown` e `KubeSchedulerDown`. Esses componentes são gerenciados no cluster mestre, portanto, é possível ignorar esses alertas.

Alerta de exemplo:
```
alerta: KubeControllerManagerDown
expr: absent(up{job="kube-controllers"}
  == 1)
para: 15m
rótulos:
severidade: crítico
anotações:
  mensagem: o KubeControllerManager desapareceu da descoberta de destino do Prometheus.
```
{: screen}
