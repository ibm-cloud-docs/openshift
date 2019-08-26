---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, scc, security context constraint, psp

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


# Configurando restrições de contexto de segurança
{: #openshift_scc}

Com restrições de contexto de segurança (SCCs), é possível controlar as ações e o acesso que os pods em seu cluster do {{site.data.keyword.openshiftlong}} podem executar. Para obter mais informações sobre SCCs, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).
{: shortdesc}

**Por que configurar minhas restrições de contexto de segurança?**</br>
Como um administrador de cluster, você deseja controlar o que acontece em seu cluster, especialmente as ações que afetam a segurança ou a prontidão do cluster. As restrições de contexto de segurança podem ajudar a controlar quais ações e acesso os pods em seu contêiner têm, como o uso de contêineres privilegiados, namespaces raiz, rede de host e portas, tipos de volume, sistemas de arquivo de host, permissões do Linux como somente leitura ou IDs do grupo e mais.

Tentando controlar quais usuários têm acesso ao seu cluster? Consulte [Designando acesso ao cluster](/docs/openshift?topic=containers-users) para configurar as permissões do {{site.data.keyword.cloud_notm}} IAM e de infraestrutura.
{: tip}

**Alguma SCC é configurada por padrão?**</br>
Por padrão, os clusters Red Hat OpenShift on IBM Cloud incluem um conjunto padrão de [SCCs do OpenShift](#oc_sccs). Além disso, os clusters têm [SCCs IBM](#ibm_sccs) que lembram muito as [políticas de segurança de pod do Kubernetes dos clusters do Kubernetes da comunidade no {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-psp#ibm_psp). Essas SCCs IBM são incluídas para melhor portabilidade com os pacotes do {{site.data.keyword.cloud_notm}} Private, como Cloud Paks.

**Em vez disso, posso usar as políticas de segurança de pod do Kubernetes?**</br>
Não. [As políticas de segurança de pod do Kubernetes ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/policy/pod-security-policy/) (PSPs) são baseadas originalmente nas SCCs do OpenShift. Entretanto, o OpenShift 3.11 suporta somente SCCs, não PSPs.

As SCCs padrão do OpenShift são mais estritas que os PSPs padrão nos clusters Kubernetes da comunidade. Dessa forma, as implementações de app que são executadas em clusters Kubernetes da comunidade podem precisar de modificação para serem executadas no OpenShift.

<br />


## Customizando restrições de contexto de segurança
{: #customize_sccs}

Para criar, editar, listar, excluir e, de outra forma, gerenciar restrições de contexto de segurança, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html). Também é possível incluir usuários ou grupos nas restrições de contexto de segurança padrão.
{: shortdesc}

<br />


## Restrições de contexto de segurança padrão do OpenShift
{: #oc_sccs}

Os clusters do Red Hat OpenShift on IBM Cloud são fornecidos com as restrições de contexto de segurança a seguir por padrão.
{: shortdesc}

Não edite as configurações existentes das SCCs do OpenShift ou da IBM, exceto para os campos `priority`, `users` ou `groups`.
{: note}

|Nome da SCC | Descrição |
|---------|-------------|
| `anyuid`| Nega o acesso semelhante à SCC `restricted`, mas permite que os usuários sejam executados com qualquer UID e qualquer GID.|
| `hostaccess`| Permite acesso a todos os namespaces de host, mas ainda requer que os pods sejam executados com um UID e contexto SELinux alocados para o namespace.<p class="important">Conceda essa SCC somente para os pods confiáveis que requerem acesso ao host a namespaces, sistemas de arquivos e IDs do processo.</p>|
| `hostmount-anyuid` | Nega o acesso semelhante à SCC `restricted`, mas permite que montagens de host e qualquer UID por um pod. Essa SCC é principalmente usada pelo reciclador de volume persistente.<p class="important">Conceda essa SCC somente para pods que requeiram acesso ao sistema do arquivo host como qualquer UID, incluindo UID 0.</p>|
| `hostnetwork`| Permite o uso da rede do host e portas do host, mas ainda requer que os pods sejam executados com um UID e um contexto de SELinux que são alocados para o namespace.<p class="important">Conceda essa SCC somente para pods que requeiram acesso à rede do host.</p>|
| `node-exporter`| Fornece o acesso apropriado para o exportador do nó Prometheus integrado. |
| `nonroot`| Nega o acesso semelhante à SCC `restricted`, mas permite que os usuários sejam executados com qualquer UID não raiz. O usuário ou o manifest do tempo de execução do contêiner deve especificar o UID.|
| `privileged`| Permite o acesso a todos os recursos privilegiados e do host e a capacidade de ser executado como qualquer usuário, grupo, fsGroup e com qualquer contexto de SELinux.<p class="important">Conceda essa SCC somente para administração de cluster que requeira o máximo de acesso possível.</p>|
| `restricted`| Nega o acesso a todos os recursos do host e requer que os pods sejam executados com um UID e um contexto do SELinux que são alocados para o namespace. Essa é a SCC mais restritiva e é usada por padrão para usuários autenticados.|
{: caption="Restrições de contexto de segurança padrão do OpenShift" caption-side="top"}

<br />


## Restrições padrão de contexto de segurança da IBM
{: #ibm_sccs}

Os clusters do Red Hat OpenShift on IBM Cloud são fornecidos com as restrições de contexto de segurança da IBM a seguir por padrão.
{: shortdesc}

Não edite as configurações existentes das SCCs do OpenShift ou da IBM, exceto para os campos `priority`, `users` ou `groups`.
{: note}

|Nome da SCC | Descrição |
|---------|-------------|
| `ibm-anyuid-hostaccess-scc`| Permite que os pods sejam executados com qualquer UID e GID, qualquer volume e acesso integral ao host.<p class="important">Conceda essa SCC somente para os pods que requeiram acesso integral ao host e à rede.</p>|
| `ibm-anyuid-hostpath-scc`| Permite que os pods sejam executados com qualquer UID e GID e qualquer volume, incluindo o caminho do host.<p class="important">Conceda essa SCC somente para pods que requeiram acesso aos volumes `hostPath`.</p>|
| `ibm-anyuid-scc` | Permite que os pods sejam executados com qualquer UID e GID, mas impede o acesso ao host.|
| `ibm-privileged-scc`| Concede acesso a todos os recursos de host privilegiados e permite que um pod seja executado com qualquer UID e GID e qualquer volume.<p class="important">Conceda essa SCC somente para administração de cluster que requeira o máximo de acesso possível.</p> |
{: caption="Restrições padrão de contexto de segurança da IBM" caption-side="top"}
