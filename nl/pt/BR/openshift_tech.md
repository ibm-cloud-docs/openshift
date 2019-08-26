---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, roks, rhoks, rhos, compliance, security standards

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

# Arquitetura de serviço
{: #openshift-service-arch}

O diagrama e a tabela a seguir descrevem os componentes padrão configurados em uma arquitetura {{site.data.keyword.openshiftlong}}.
{: shortdesc}

Para obter mais informações sobre a arquitetura do OpenShift Container Platform, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/architecture/index.html).
{: note}

![Arquitetura de cluster do Red Hat OpenShift on IBM Cloud](/images/cs_org_ov_both_ses_rhos.png)

Role pela tabela a seguir para obter mais informações sobre os componentes do cluster mestre e do nó do trabalhador.

| Componentes principais| Descrição |
|:-----------------|:-----------------|
| Réplicas | Os componentes principais, incluindo o servidor da API do OpenShift Kubernetes e o armazenamento de dados etcd, têm três réplicas e, se localizados em uma área metropolitana de multizona, são difundidos entre as zonas para disponibilidade ainda mais alta. Os componentes principais são submetidos a backup a cada 8 horas.|
| `rhos-api` | O servidor da API do OpenShift Kubernetes serve como o ponto de entrada principal para todas as solicitações de gerenciamento de cluster do nó do trabalhador para o principal. O servidor da API valida e processa solicitações que mudam o estado de recursos do Kubernetes, como pods ou serviços, e armazena esse estado no armazenamento de dados etcd.|
| `openvpn-server` | O servidor OpenVPN funciona com o cliente OpenVPN para conectar com segurança o mestre ao nó do trabalhador. Essa conexão suporta chamadas `apiserver proxy` para seus pods e serviços e chamadas `oc exec`, `attach` e `logs` para o kubelet.|
| `etcd` | etcd é um armazenamento de valores de chaves altamente disponível que armazena o estado de todos os recursos do Kubernetes de um cluster, como serviços, implementações e pods. Os dados em etcd são submetidos a backup para uma instância de armazenamento criptografada que a IBM gerencia.|
| `rhos-controller` | O gerenciador do controlador do OpenShift observa os pods recém-criados e decide onde implementá-los com base na capacidade, necessidades de desempenho, restrições de política, especificações de antiafinidade e requisitos de carga de trabalho. Se não puder ser localizado nenhum nó do trabalhador que corresponda aos requisitos, o pod não será implementado
no cluster. O controlador também observa o estado de recursos de cluster, como conjuntos de réplicas. Quando o estado de um recurso for alterado, por exemplo, se um pod em um conjunto de réplicas ficar inativo, o gerenciador do controlador iniciará as ações de correção para atingir o estado necessário. O `rhos-controller` funciona como o planejador e o gerenciador de controlador em uma configuração do Kubernetes da comunidade. |
| `cloud-controller-manager` | O gerenciador do controlador de nuvem gerencia componentes específicos do provedor em nuvem, como o balanceador de carga do {{site.data.keyword.cloud_notm}}.|
| Controladores de Admissão | Os controladores de admissão são implementados para recursos específicos no OpenShift e no {{site.data.keyword.containerlong_notm}}. Com os controladores de admissão, é possível configurar políticas em seu cluster que determinam se uma ação específica no cluster é permitida ou não. Na política, é possível especificar condições quando um usuário não pode executar uma ação, mesmo que essa ação faça parte das permissões gerais que você designou ao usuário usando RBAC. Portanto, os controladores de admissão podem fornecer uma camada adicional de segurança para seu cluster antes que uma solicitação de API seja processada pelo servidor de API do Kubernetes. </br></br> Ao criar um cluster do OpenShift, o {{site.data.keyword.containerlong_notm}} instala automaticamente os [controladores de admissão do Kubernetes ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/admin/admission-controllers/) a seguir na ordem determinada no mestre do Kubernetes, que não pode ser mudada pelo usuário:<ul><li>`NamespaceLifecycle`</li><li>`LimitRanger`</li><li>`ServiceAccount`</li><li>`Classe DefaultStorageClass`</li><li>`ResourceQuota`</li><li>`StorageObjectInUseProtection`</li><li>`PersistentVolumeClaimResize`</li><li>[`Prioridade`](/docs/containers?topic=containers-pod_priority#pod_priority)</li><li>`BuildByStrategy`</li><li>`OriginPodNodeEnvironment`</li><li>`PodNodeSelector`</li><li>`ExternalIPRanger`</li><li>`NodeRestriction`</li><li>`SecurityContextConstraint`</li><li>`SCCExecRestrictions`</li><li>`PersistentVolumeLabel`</li><li>`OwnerReferencesPermissionEnforcement`</li><li>`PodTolerationRestriction`</li><li>`openshift.io/JenkinsBootstrapper`</li><li>`openshift.io/BuildConfigSecretInjector`</li><li>`openshift.io/ImageLimitRange`</li><li>`openshift.io/RestrictedEndpointsAdmission`</li><li>`openshift.io/ImagePolicy`</li><li>`openshift.io/IngressAdmission`</li><li>`openshift.io/ClusterResourceQuota`</li><li>`MutatingAdmissionWebhook`</li><li>`ValidatingAdmissionWebhook`</li></ul></br><p>É possível [instalar seus próprios controladores de admissão no cluster ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks) ou escolher entre os controladores de admissão opcionais que o {{site.data.keyword.containerlong_notm}} fornece.</p><ul><li><strong>[Executor de segurança de imagem de contêiner](/docs/services/Registry?topic=registry-security_enforce#security_enforce):</strong> use esse controlador de admissão para cumprir as políticas do Vulnerability Advisor em seu cluster para bloquear implementações de imagens vulneráveis.</li></ul></br><p class="note">Se você instalou manualmente os controladores de admissão e não desejar usá-los mais, certifique-se de removê-los completamente. Se os controladores de admissão não forem completamente removidos, eles poderão bloquear todas as ações que você deseja executar no cluster.</p>
{: caption="Tabela 1. Componentes principais do OpenShift." caption-side="top"}
{: #rhos-components-1}
{: tab-title="Master"}
{: tab-group="rhos-components"}
{: class="simple-tab-table"}

| Componentes do nó do trabalhador| Descrição |
|:-----------------|:-----------------|
| Sistema operacional | Os nós do trabalhador do Red Hat OpenShift on IBM Cloud são executados no sistema operacional Red Hat Enterprise Linux 7. |
| Projetos | O OpenShift organiza seus recursos em projetos, que são namespaces do Kubernetes com anotações e inclui muito mais componentes que os clusters do Kubernetes da comunidade para executar recursos do OpenShift, como o catálogo. Os componentes selecionados de projetos são descritos nas linhas a seguir. Para obter mais informações, consulte [Projetos e usuários ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/architecture/core_concepts/projects_and_users.html).|
| `kube-system` | Esse namespace inclui vários componentes que são usados para executar o Kubernetes no nó do trabalhador.<ul><li>**`ibm-master-proxy`**: o `ibm-master-proxy` é um conjunto de daemon que encaminha as solicitações do nó do trabalhador para os endereços IP das réplicas principais altamente disponíveis. Em clusters de zona única, o principal tem três réplicas em hosts separados. Para clusters que estão em uma zona com capacidade para várias zonas, o mestre tem três réplicas que são difundidas entre as zonas. Um balanceador de carga altamente disponível encaminha as solicitações para o nome de domínio principal para as réplicas principais.</li><li>**`openvpn-client`**: o cliente OpenVPN trabalha com o servidor OpenVPN para conectar de forma segura o principal ao nó do trabalhador. Essa conexão suporta chamadas `apiserver proxy` para seus pods e serviços e chamadas `oc exec`, `attach` e `logs` para o kubelet.</li><li>**`kubelet`**: o kubelet é um agente do nó do trabalhador que é executado em cada nó trabalhador e é responsável por monitorar o funcionamento de pods que são executados no nó do trabalhador e por observar os eventos que o servidor da API do Kubernetes envia. Com base nos eventos, o kubelet cria ou remove pods, assegura as análises de vivacidade e prontidão e relata de volta o status dos pods para o servidor de API do Kubernetes.</li><li>**`calico`**: o Calico gerencia políticas de rede para seu cluster e inclui alguns componentes para gerenciar a conectividade de rede do contêiner, a designação de endereço IP e o controle de tráfego de rede.</li><li>**Outros componentes**: o namespace `kube-system` também inclui componentes para gerenciar recursos fornecidos pela IBM, tais como plug-ins de armazenamento para armazenamento de arquivo e bloco, balanceador de carga do aplicativo (ALB) do Ingress, criação de log do `fluentd` e `keepalived`.</li></ul>|
| `ibm-system` | Esse namespace inclui a implementação `ibm-cloud-provider-ip` que trabalha com `keepalived` para fornecer a verificação de funcionamento e o balanceamento de carga da Camada 4 para solicitações para os pods de app.|
| `kube-proxy-and-dns`| Esse namespace inclui os componentes para validar o tráfego de rede recebido com relação às regras `iptables` que estão configuradas no nó do trabalhador e as solicitações de proxies que podem entrar ou sair do cluster.|
| `default` | Esse namespace será usado se você não especificar um namespace ou criar um projeto para seus recursos do Kubernetes. Além disso, o namespace padrão inclui os componentes a seguir para suportar seus clusters do OpenShift.<ul><li>**`router`**: o OpenShift usa [rotas ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html) para expor o serviço de um app em um nome de host para que os clientes externos possam acessar o serviço. O roteador mapeia o serviço para o nome do host.</li><li>**`docker-registry`** e **`registry-console`**: o OpenShift fornece um [registro de imagem de contêiner ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html) interno que pode ser usado para gerenciar e visualizar localmente imagens por meio do console. Como alternativa, é possível configurar o {{site.data.keyword.registrylong_notm}} privado.</li></ul>|
| Outros projetos | Outros componentes são instalados em vários namespaces por padrão para ativar a funcionalidade, como criação de log, monitoramento e o console do OpenShift.<ul><li><code>ibm-cert-store</code></li><li><code>kube-public</code></li><li><code>kube-service-catalog</code></li><li><code>openshift</code></li><li><code>openshift-ansible-service-broker</code></li><li><code>openshift-console</code></li><li><code>openshift-infra</code></li><li><code>openshift-monitoring</code></li><li><code>openshift-node</code></li><li><code>openshift-template-service-broker</code></li><li><code>openshift-web-console</code></li></ul>|
{: caption="Tabela 2. Componentes do nó do trabalhador do OpenShift." caption-side="top"}
{: #rhos-components-2}
{: tab-title="Worker nodes"}
{: tab-group="rhos-components"}
{: class="simple-tab-table"}
