---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: oks, iro, openshift, red hat, red hat openshift, rhos, roks, rhoks

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

# Criação de log e monitoramento
{: #openshift_health}



Para métricas de cluster e criação de log e monitoramento de apps, os clusters do {{site.data.keyword.openshiftlong}} incluem ferramentas integradas para ajudar a gerenciar o funcionamento de sua única instância de cluster. Também é possível configurar ferramentas do {{site.data.keyword.cloud_notm}} para análise de vários clusters ou outros casos de uso, como complementos do {{site.data.keyword.containerlong_notm}}: {{site.data.keyword.la_full_notm}} e {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

## Usando a pilha de criação de log e monitoramento integrada do OpenShift
{: #openshift_logmet}

Por padrão, os clusters do Red Hat OpenShift on IBM Cloud são implementados com ferramentas de criação de log e monitoramento integradas que são baseadas em projetos de software livre, como Prometheus, Elasticsearch, Fluentd e Kibana. Para obter mais informações, consulte os docs do OpenShift a seguir.
{: shortdesc}

* [Monitoramento de cluster do Prometheus ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/install_config/prometheus_cluster_monitoring.html).
* [Agregando logs de contêiner ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging.html).
* [Diretrizes de dimensionamento de criação de log agregadas ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging_sizing.html).
* [Ativando métricas de cluster ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/install_config/cluster_metrics.html).

<br />


## Configurando complementos LogDNA e Sysdig para monitorar o funcionamento do cluster
{: #openshift_logdna_sysdig}

Como o OpenShift configura, por padrão, [Restrições de contexto de segurança (SCC) ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html) mais estritas que o Kubernetes da comunidade, talvez você ache que alguns apps ou complementos de cluster que você usa no Kubernetes da comunidade não possam ser implementados no OpenShift da mesma forma. Especialmente, muitas imagens devem ser executadas como um usuário `root` ou como um contêiner privilegiado, o que é impedido no OpenShift por padrão. É possível modificar as SCCs padrão criando contas de segurança privilegiadas e atualizando o `securityContext` na especificação de pod para usar dois complementos populares do {{site.data.keyword.containerlong_notm}}: {{site.data.keyword.la_full_notm}} e {{site.data.keyword.mon_full_notm}}.
{: shortdesc}

Antes de iniciar, efetue login em seu cluster como um administrador.
1.  Abra seu console do OpenShift em `https://<master_URL>/console`. Por exemplo, `https://c0.containers.cloud.ibm.com:23652/console`.
2.  Na barra de menus do console da web do OpenShift, clique em seu perfil **IAM#user.name@email.com > Copiar comando de login** e cole o comando de login copiado `oc` em seu terminal para autenticar por meio da CLI.
3.  Configure o [{{site.data.keyword.la_short}}](#openshift_logdna) e o [{{site.data.keyword.mon_short}}](#openshift_sysdig).

<br />


### Configurando o LogDNA
{: #openshift_logdna}

Configure um projeto e uma conta de serviço privilegiado para o {{site.data.keyword.la_full_notm}}. Em seguida, crie uma instância do {{site.data.keyword.la_short}} em sua conta do {{site.data.keyword.cloud_notm}}. Para integrar sua instância do {{site.data.keyword.la_short}} ao seu cluster do OpenShift, deve-se modificar o conjunto de daemon que é implementado para usar a conta de serviço privilegiado para executar como raiz.
{: shortdesc}

1.  Configure o projeto e a conta de serviço privilegiado para o LogDNA.
    1.  Como um administrador de cluster, crie um projeto `logdna`.
        ```
        oc adm new-project logdna
        ```
        {: pre}
    2.  Tenha o projeto como destino para que os recursos subsequentes que você criar estejam no namespace do projeto `logdna`.
        ```
        oc project logdna
        ```
        {: pre}
    3.  Crie uma conta de serviço para o projeto `logdna`.
        ```
        oc create serviceaccount logdna
        ```
        {: pre}
    4.  Inclua uma restrição de contexto de segurança privilegiada para a conta de serviço para o projeto `logdna`.<p class="note">Se você desejar verificar qual autorização a política SCC `privileged` fornece à conta de serviço, execute `oc describe scc privileged`. Para obter mais informações sobre SCCs, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).</p>
        ```
        oc adm policy add-scc-to-user privileged -n logdna -z logdna
        ```
        {: pre}
2.  Crie sua instância do {{site.data.keyword.la_full_notm}} no mesmo grupo de recursos que seu cluster. Selecione um plano de precificação que determina o período de retenção para seus logs, como `lite`, que retém logs por 0 dias. A região não tem que corresponder à região de seu cluster. Para obter mais informações, consulte [Provisionando uma instância](/docs/services/Log-Analysis-with-LogDNA/tutorials?topic=LogDNA-provision) e [Planos de precificação](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-about#overview_pricing_plans).
    ```
    ibmcloud resource service-instance-create <service_instance_name> logdna (lite|7-days|14-days|30-days) <region> [-g <resource_group>]
    ```
    {: pre}

    Exemplo de comando:
    ```
    ibmcloud resource service-instance-create logdna-openshift logdna lite us-south
    ```
    {: pre}

    Na saída, anote o **ID** da instância de serviço, que está no formato `crn:v1:bluemix:public:logdna:<region>:<ID_string>::`.
    ```
    A instância de serviço <name> foi criada.

    Nome: <name>   
    ID: crn:v1:bluemix:public:logdna:<region>:<ID_string>::   
    GUID: <guid>   
    Local: <region>   
    ...
    ```
    {: screen}    
3.  Obtenha sua chave de ingestão da instância do {{site.data.keyword.la_short}}. A chave de ingestão do LogDNA é usada para abrir um soquete seguro da web para o servidor de ingestão do LogDNA e para autenticar o agente de criação de log com o serviço {{site.data.keyword.la_short}}.
    1.  Crie uma chave de serviço para sua instância do LogDNA.
        ```
        ibmcloud resource service-key-create <key_name> Administrator --instance-id <logdna_instance_ID>
        ```
        {: pre}
    2.  Anote o **ingestion_key** de sua chave de serviço.
        ```
        ibmcloud resource service-key <key_name>
        ```
        {: pre}

        Saída de exemplo:
        ```
        Nome: <key_name>  
        ID: crn:v1:bluemix:public:logdna:<region>:<ID_string>::    
        Criado em: Thu Jun 6 21:31:25 UTC 2019   
        Estado: ativo   
        Credenciais:                                   
                       apikey: <api_key_value>      
                       iam_apikey_description: gerado automaticamente para a chave <ID>     
                       iam_apikey_name: <key_name>       
                       iam_role_crn: crn:v1:bluemix:public:iam::::role:Administrator      
                       iam_serviceid_crn: crn:v1:bluemix:public:iam-identity::<ID_string>     
                       ingestion_key:            111a11aa1a1a11a1a11a1111aa1a1a11    
        ```
        {: screen}
4.  Crie um segredo do Kubernetes para armazenar sua chave de ingestão do LogDNA para sua instância de serviço.
    ```
     oc create secret generic logdna-agent-key --from-literal=logdna-agent-key=<logDNA_ingestion_key>
    ```
    {: pre}
5.  Crie um daemon do Kubernetes configurado para implementar o agente LogDNA em cada nó do trabalhador do seu cluster do OpenShift. O agente LogDNA coleta logs com a extensão `*.log` e arquivos sem extensão que são armazenados no diretório `/var/log` do seu pod. Por padrão, os logs são coletados de todos os namespaces, incluindo `kube-system` e encaminhados automaticamente para o serviço do {{site.data.keyword.la_short}}.
    ```
    oc create -f https://raw.githubusercontent.com/logdna/logdna-agent/master/logdna-agent-ds-os.yml
    ```
    {: pre}
6.  Verifique se o pod `logdna-agent` em cada nó está em um status **Em execução**.
    ```
    oc get pods
    ```
    {: pre}
7.  No console do **Observabilidade > Criação de log** do [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/observe/logging), na linha para sua instância do {{site.data.keyword.la_short}}, clique em **Visualizar o LogDNA**. O painel do LogDNA é aberto. Após alguns minutos, os logs do seu cluster são exibidos e é possível analisar seus logs.

Para obter mais informações sobre como usar o {{site.data.keyword.la_short}}, consulte os [docs de Próximas etapas](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-kube#kube_next_steps).

<br />


### Configurando o Sysdig
{: #openshift_sysdig}

Crie uma instância do {{site.data.keyword.mon_full_notm}} em sua conta do {{site.data.keyword.cloud_notm}}. Para integrar sua instância do {{site.data.keyword.mon_short}} ao seu cluster do OpenShift, deve-se executar um script que crie um projeto e uma conta de serviço privilegiado para o agente Sysdig.
{: shortdesc}

1.  Crie sua instância do {{site.data.keyword.mon_full_notm}} no mesmo grupo de recursos que seu cluster. Selecione um plano de precificação que determine o período de retenção para seus logs, como `lite`. A região não tem que corresponder à região de seu cluster. Para obter mais informações, consulte [Provisionando uma instância](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-provision).
    ```
    ibmcloud resource service-instance-create <service_instance_name> sysdig-monitor (lite|graduated-tier) <region> [-g <resource_group>]
    ```
    {: pre}

    Exemplo de comando:
    ```
    ibmcloud resource service-instance-create sysdig-openshift sysdig-monitor lite us-south
    ```
    {: pre}

    Na saída, anote o **ID** da instância de serviço, que está no formato `crn:v1:bluemix:public:logdna:<region>:<ID_string>::`.
    ```
    A instância de serviço <name> foi criada.

    Nome: <name>   
    ID: crn:v1:bluemix:public:sysdig-monitor:<region>:<ID_string>::   
    GUID: <guid>   
    Local: <region>   
    ...
    ```
    {: screen}    
2.  Obtenha sua chave de acesso da instância do {{site.data.keyword.mon_short}}. A chave de acesso do Sysdig é usada para abrir um soquete seguro da web para o servidor de ingestão do Sysdig e para autenticar o agente de monitoramento com o serviço {{site.data.keyword.mon_short}}.
    1.  Crie uma chave de serviço para sua instância do Sysdig.
        ```
        ibmcloud resource service-key-create <key_name> Administrator --instance-id <sysdig_instance_ID>
        ```
        {: pre}
    2.  Anote a **Chave de acesso do Sysdig** e o **Terminal do coletor do Sysdig** de sua chave de serviço.
        ```
        ibmcloud resource service-key <key_name>
        ```
        {: pre}

        Saída de exemplo:
        ```
        Nome: <key_name>  
        ID: crn:v1:bluemix:public:sysdig-monitor:<region>:<ID_string>::    
        Criado em: Thu Jun 6 21:31:25 UTC 2019   
        Estado: ativo   
        Credenciais:                                   
                       Sysdig Access Key:           11a1aa11-aa1a-1a1a-a111-11a11aa1aa11      
                       Sysdig Collector Endpoint:   ingest.<region>.monitoring.cloud.ibm.com      
                       Sysdig Customer Id:          11111      
                       Sysdig Endpoint:             https://<region>.monitoring.cloud.ibm.com  
                       apikey: <api_key_value>      
                       iam_apikey_description: gerado automaticamente para a chave <ID>     
                       iam_apikey_name: <key_name>       
                       iam_role_crn: crn:v1:bluemix:public:iam::::role:Administrator      
                       iam_serviceid_crn: crn:v1:bluemix:public:iam-identity::<ID_string>       
        ```
        {: screen}
3.  Execute o script para configurar um projeto `ibm-observe` com uma conta de serviço privilegiado e um conjunto de daemon do Kubernetes para implementar o agente Sysdig em cada nó do trabalhador de seu cluster Kubernetes. O agente Sysdig coleta métricas, como o uso de CPU do nó do trabalhador, o uso de memória do nó do trabalhador, o tráfego HTTP para e de seus contêineres e os dados sobre vários componentes de infraestrutura.

    No comando a seguir, substitua <code>&lt;sysdig_access_key&gt;</code> e <code>&lt;sysdig_collector_endpoint&gt;</code> pelos valores da chave de serviço que você criou anteriormente. Para <code>&lt;tag&gt;</code>, é possível associar tags a seu agente Sysdig, como `role:service,location:us-south` para ajudar a identificar o ambiente do qual as métricas são provenientes.

    ```
    curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a <sysdig_access_key> -c <sysdig_collector_endpoint> -t <tag> -ac 'sysdig_capture_enabled: false' --openshift
    ```
    {: pre}

    Saída de exemplo:
    ```
    * Detectando o sistema operacional
    * Fazendo download do yaml da função de cluster do Sysdig
    * Fazendo download do yaml do mapa de configuração do Sysdig
    * Fazendo download do yaml do daemonset v2 do Sysdig
    * Criando o projeto: ibm-observe
    * Criando o sysdig-agent serviceaccount no projeto: ibm-observe
    * Criando políticas de acesso do sysdig-agent
    * Criando o segredo do sysdig-agent usando o ACCESS_KEY fornecido
    * Recuperando o ID do cluster do IKS e o nome do cluster
    * Configurando o nome do cluster como <cluster_name>
    * Configurando ibm.containers-kubernetes.cluster.id 1fbd0c2ab7dd4c9bb1f2c2f7b36f5c47
    * Atualizando o configmap do agente e aplicando ao cluster
    * Configurando tags
    * Configurando o terminal do coletor
    * Incluindo configuração adicional no dragent.yaml
    * Ativando o
    configmap/sysdig-agent do Prometheus criado
    * Implementando o
    daemonset.extensions/sysdig-agent do agente sysdig criado
    ```
    {: screen}

4.  Verifique se os pods `sydig-agent` em cada nó mostram que os pods **1/1** estão prontos e se cada pod tem um status **Em execução**.
    ```
    oc get pods
    ```
    {: pre}

    Saída de exemplo:
    ```
    NAME                 READY     STATUS    RESTARTS   AGE
    sysdig-agent-qrbcq   1/1       Running   0          1m
    sysdig-agent-rhrgz   1/1       Running   0          1m
    ```
    {: screen}
5.  No console **Observabilidade > Monitoramento** do [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/observe/logging), na linha para sua instância do {{site.data.keyword.mon_short}}, clique em **Visualizar Sysdig**. O painel do Sysdig é aberto e é possível analisar suas métricas do cluster.

Para obter mais informações sobre como usar o {{site.data.keyword.mon_short}}, consulte os [docs de Próximas etapas](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-kubernetes_cluster#kubernetes_cluster_next_steps).

<br />


### Opcional: limpando
{: #openshift_logdna_sysdig_cleanup}

Remova as instâncias do {{site.data.keyword.la_short}} e do {{site.data.keyword.mon_short}} de seu cluster e da conta do {{site.data.keyword.cloud_notm}}. Observe que, a menos que você armazene os logs e as métricas no [armazenamento persistente](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-archiving), não é possível acessar essas informações depois de excluir as instâncias de sua conta.
{: shortdesc}

1.  Limpe as instâncias do {{site.data.keyword.la_short}} e do {{site.data.keyword.mon_short}} em seu cluster removendo os projetos que você criou para eles. Quando você exclui um projeto, seus recursos, como contas de serviço e conjuntos de daemon, também são removidos.
    ```
    oc delete project logdna
    ```
    {: pre}
    ```
    oc delete project ibm-observe
    ```
    {: pre}
2.  Remova as instâncias de sua conta do {{site.data.keyword.cloud_notm}}.
    *   [Removendo uma instância do {{site.data.keyword.la_short}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-remove).
    *   [Removendo uma instância do {{site.data.keyword.mon_short}}](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-remove).

<br />


## Configurando ferramentas de criação de log e de monitoramento do {{site.data.keyword.cloud_notm}}
{: #openshift_other_logmet}

Para obter mais informações sobre outras ferramentas de criação de log e monitoramento que podem ser configuradas, incluindo serviços do {{site.data.keyword.cloud_notm}}, consulte os tópicos a seguir nos docs do {{site.data.keyword.containershort_notm}}.
{: shortdesc}

* [Escolhendo uma solução de criação de log](/docs/containers?topic=containers-health#logging_overview).
* [Escolhendo uma solução de monitoramento](/docs/containers?topic=containers-health#view_metrics).
