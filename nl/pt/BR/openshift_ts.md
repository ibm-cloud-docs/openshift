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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# Resolvendo problemas de clusters do OpenShift
{: #openshift_troubleshoot}

Revise alguns problemas conhecidos ou mensagens de erro comuns que você pode encontrar ao usar clusters do {{site.data.keyword.openshiftlong}}.
{: shortdesc}

Para depuração de cluster geral, consulte os docs do {{site.data.keyword.containerlong_notm}}:
* [Depurando seu cluster](/docs/containers?topic=containers-cs_troubleshoot)
* [Clusters e nós do trabalhador](/docs/containers?topic=containers-cs_troubleshoot_clusters)
* [Storage](/docs/containers?topic=containers-cs_troubleshoot_storage)
* [Criação de log e monitoramento](/docs/containers?topic=containers-cs_troubleshoot_health)
* [Depurando o Ingresso](/docs/containers?topic=containers-cs_troubleshoot_debug_ingress)
* [Rede de cluster](/docs/containers?topic=containers-cs_troubleshoot_network)

## Feedback e perguntas
{: #openshift_support}

Os clusters do Red Hat OpenShift on IBM Cloud em disponibilidade geral são suportados pelo suporte IBM. Se você tiver clusters beta restantes, [crie clusters do OpenShift padrão](/docs/openshift?topic=openshift-openshift-create-cluster) antes de os clusters beta expirarem.
{: shortdesc}

Para qualquer pergunta ou feedback, poste no Slack.
*   Se você for um usuário externo, poste no canal [#openshift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-container-service.slack.com/messages/CKCJLJCH4).
*   Se você for um IBMista, use o canal [#iks-openshift-users ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-argonauts.slack.com/messages/CJH0UPN2D).

Se você não usa um IBMid para a sua conta do {{site.data.keyword.cloud_notm}}, [solicite um convite](https://bxcs-slack-invite.mybluemix.net/) para esse Slack.
{: tip}

## Permissões ausentes para criar clusters
{: #rhoks_ts_cluster_permissions}

{: tsSymptoms}
Você não tem permissões para criar um cluster.

{: tsCauses}
Para criar um cluster do OpenShift, deve-se ter as mesmas permissões que você precisa para criar um cluster Kubernetes da comunidade. As permissões necessárias incluem credenciais de infraestrutura para a região e permissões de **Administrador** do grupo de recursos e do {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).

{: tsResolve}
Revise [Designando acesso ao cluster](/docs/openshift?topic=openshift-users) para saber como configurar credenciais de infraestrutura para uma região e um grupo de recursos e como designar acesso aos usuários por meio do IAM.

<br />


## Nenhum recurso encontrado
{: #rhoks_ts_not_found}

{: tsSymptoms}
Quando estiver executando um comando `oc`, como `oc get nodes` ou `oc get secrets`, você verá uma mensagem de erro semelhante à mostrada a seguir.

```
No resources found.
```
{: screen}

{: tsCauses}
Seu token do OpenShift expirou. Os tokens do OpenShift que são gerados usando suas credenciais do {{site.data.keyword.cloud_notm}} IAM expiram em 24 horas.

{: tsResolve}
[Autentique-se novamente com o token do OpenShift](/docs/openshift?topic=openshift-openshift-cli#openshift_cluster_login) copiando o comando `oc login` do console da web ou criando uma chave de API.

<br />


## Erro do servidor OpenVPN devido ao endereço IP de ingresso para NLB
{: #rhoks_ts_openvpn_subnet}

{: tsSymptoms}
Você vê a mensagem de erro a seguir.
```
CAE003: não é possível determinar o endereço IP do ingresso para o balanceador de carga de rede.
```
{: screen}

{: tsCauses}
O servidor OpenVPN não pôde ser configurado porque o endereço IP do roteador que é criado para o balanceador de carga de rede (NLB) não pôde ser localizado. O roteador pode não ter sido designado a um endereço IP porque seu cluster não tem uma sub-rede com endereços IP móveis disponíveis ou a configuração do NLB não foi concluída.

{: tsResolve}

**Verifique se seu cluster possui sub-redes disponíveis.**
1.  Verifique se o seu cluster possui um **CIDR de sub-rede** para sub-redes públicas e privadas. Se você configurar um cluster somente VLAN privado, poderá ter somente uma sub-rede privada.
    ```
    ibmcloud oc cluster-get --cluster <cluster_name_or_ID> --showResources
    ```
    {: pre}

    Saída de exemplo:
    ```
    Name: <cluster_name>   
    ...

    VLANs de sub-rede
    ID de VLAN   CIDR de sub-rede        Público   Gerenciado pelo usuário   
    2345678   10.xxx.xx.xxx/29   false    false   
    2876543   169.xx.xxx.xxx/29  true     false
    ```
    {: screen}
2.  Se o cluster não tiver uma sub-rede, [crie uma sub-rede para o cluster](/docs/containers?topic=containers-subnets#request) ou [inclua uma sub-rede existente de sua conta no cluster](/docs/containers?topic=containers-subnets#add-existing).
3.  Se o cluster tiver uma sub-rede, [verifique endereços IP móveis disponíveis](/docs/containers?topic=containers-subnets#review_ip) e, se necessário, [inclua mais endereços IP móveis incluindo uma sub-rede](/docs/containers?topic=containers-subnets#adding_ips).
4.  Atualize o mestre para reiniciar a configuração do OpenVPN para que ele use a sub-rede disponível.
    ```
    ibmcloud oc cluster-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

**Verifique se a configuração do NLB foi concluída com sucesso.**
1.  Verifique se os pods `ibm-cloud-provider-ip-*` para o NLB estão em um status **Em execução**.
    ```
    oc get pods -n ibm-system | grep ibm-cloud-provider-ip
    ```
    {: pre}
2.  Se um pod não estiver em execução, revise os **Eventos** nos detalhes do pod para solucionar o problema.
    ```
    oc describe pod -n kube-system <pod_name>
    ```
    {: pre}
3.  Após resolver o problema do pod do NLB, atualize o mestre para reiniciar a configuração do NLB.
    ```
    ibmcloud oc cluster-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />


## Erro do servidor OpenVPN devido ao DNS do NLB
{: #rhoks_ts_openvpn_dns}

{: tsSymptoms}
Não foi possível criar um domain name service para o balanceador de carga de rede (`ibmcloud oc nlb-dns-create`) com a mensagem de erro a seguir:<ul>
<li><code>Esta ação requer a função Editor para o cluster no IBM Cloud Container Service. Entre em contato com o administrador de conta do IBM Cloud e solicite a função de usuário de Identidade e acesso necessária. (A0008)</code></li>
<li><code>O cluster especificado não pôde ser localizado. (A0006)</code></li>
<li><code>Os parâmetros de entrada no corpo da solicitação estão incompletos ou no formato errado. Assegure-se de incluir todos os parâmetros necessários em sua solicitação no formato JSON. (E0011)</code></li></ul>

{: tsCauses}
O servidor OpenVPN não pôde ser configurado porque um domain name service (DNS) não foi criado para o balanceador de carga de rede (NLB).

{: tsResolve}
1.  Verifique se você tem as permissões corretas no {{site.data.keyword.cloud_notm}} IAM. Se não tiver, entre em contato com seu administrador de conta para [designar a plataforma do IAM apropriada ou a função de acesso ao serviço](/docs/containers?topic=containers-users#platform).
    ```
    ibmcloud iam user-policies <my_user_name@example.com>
    ```
    {: pre}
2.  Para erros de cluster não localizado ou parâmetro de entrada incorreto, continue na próxima etapa.
3.  Atualize o mestre para que a operação de criação de DNS do NLB seja tentada novamente.
    ```
    ibmcloud oc cluster-refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />


## Erro de servidor VPN devido a credenciais de infraestrutura
{: #rhoks_ts_openvpn_login}

{: tsSymptoms}
Após criar ou atualizar um cluster, o status do mestre retorna uma mensagem de erro de configuração do servidor de VPN semelhante à mostrada a seguir.
```
Falha na atualização da configuração do servidor de VPN. O suporte do IBM Cloud foi notificado e está trabalhando para resolver esse problema.
```
{: screen}

{: tsCauses}
As credenciais de infraestrutura associadas ao grupo de recursos em que o cluster é criado estão ausentes (por exemplo, o proprietário da chave de API não é mais parte da conta) ou as permissões necessárias estão ausentes.

{: tsResolve}
[Conclua o guia de resolução de problemas](/docs/containers?topic=containers-cs_troubleshoot_clusters#cs_credentials) para verificar e atualizar as credenciais de infraestrutura usadas para o grupo de recursos.

<br />


## Os projetos ausentes ou comandos `oc` e `kubectl` falham
{: #rhoks_ts_admin_config}

{: tsSymptoms}
Você não vê todos os projetos aos quais tem acesso. Quando você tenta executar comandos `oc` ou `kubectl`, você vê um erro semelhante ao mostrado a seguir.
```
No resources found.
Error from server (Forbidden): <resource> is forbidden: User "IAM#user@email.com" cannot list <resources> at the cluster scope: no RBAC policy matched
```
{: screen}

{: tsCauses}
É necessário fazer download dos arquivos de configuração `admin` para seu cluster a fim de executar comandos que requerem a função de cluster `cluster-admin`.

{: tsResolve}
Execute `ibmcloud oc cluster-config --cluster <cluster_name_or_ID> --admin` e tente novamente.

<br />


## Pods no status `CrashLoopBackOff`
{: #rhoks_ts_pods_crashloop}

{: tsSymptoms}
Seus pods estão em um status `CrashLoopBackOff`.

{: tsCauses}
Quando você tenta implementar um app que funciona nas plataformas do Kubernetes da comunidade, talvez veja esse status ou uma mensagem de erro relacionada porque o OpenShift define, por padrão, configurações de segurança mais estritas que o Kubernetes da comunidade.

{: tsResolve}
Assegure-se de ter seguido os docs no [tópico Movendo seus apps para o OpenShift](/docs/openshift?topic=openshift-openshift_apps#openshift_move_apps).

<br />


## Não é possível enviar por push ou fazer pull de imagens da máquina local para o registro do Docker
{: #rhoks_ts_docker_local}

{: tsSymptoms}
Não é possível enviar por push ou fazer pull de imagens do Docker de sua máquina local para o registro do Docker integrado do cluster.

{: tsCauses}
Por padrão, o registro do Docker está disponível internamente dentro do cluster. É possível desenvolver apps por meio de diretórios remotos, como GitHub ou DockerHub usando o comando `oc new-app`. Ou é possível expor seu registro do Docker, assim como com uma rota ou balanceador de carga para que seja possível enviar por push e fazer pull de imagens da sua máquina local.

{: tsResolve}
Crie uma rota para o serviço `docker-registry` no projeto `default`. Inclua a sinalização `--hostname` para que seja possível fornecer ao registro um nome de domínio mais curto.

```
oc create route edge --service=docker-registry -n default --hostname <registry_domain_name>
```
{: pre}
