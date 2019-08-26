---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: kubernetes, openshift, roks, rhoks, rhos

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

# Implementando apps em clusters do OpenShift
{: #openshift_apps}

Com os clusters do {{site.data.keyword.openshiftlong}}, é possível implementar apps de um arquivo remoto ou de um repositório como GitHub com um único comando. Além disso, seus clusters são fornecidos com vários serviços integrados que podem ser usados para ajudar a operar seu cluster.
{: shortdesc}

Para criar um novo app, use o comando `oc new-app`. Para obter mais informações, [teste o tutorial](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app) e consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_cli.html).

```
oc new-app --name <app_name> https://github.com/<path_to_app_repo> [--context-dir=<subdirectory>]
```
{: pre}

## Movendo seus apps para o OpenShift
{: #openshift_move_apps}

Por padrão, o OpenShift define configurações de segurança mais estritas que o Kubernetes da comunidade. Se você tiver apps que foram executados anteriormente no Kubernetes da comunidade, poderá ser necessário modificar seus apps para que seja possível implementá-los no OpenShift.
{: shortdesc}

Por exemplo, os apps que são configurados para serem executados como raiz podem falhar, com os pods em um status `CrashLoopBackOff`. Para resolver esse problema, é possível modificar as restrições de contexto de segurança padrão ou usar uma imagem que não seja executada como raiz.

Para obter mais informações, consulte os docs do OpenShift para [Gerenciar restrições de contexto de segurança (SCC) ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).

Para migrar apps do OpenShift de uma versão anterior, como da 2.x para a 3.x, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/dev_guide/migrating_applications/index.html).

<br />


## Acessando o console da web do OpenShift
{: #openshift_console}

É possível usar o console do OpenShift para gerenciar seus apps, implementar apps do catálogo e acessar a funcionalidade integrada para ajudar a operar seu cluster. O console do OpenShift é implementado em seu cluster por padrão, em vez de no painel do Kubernetes, como em clusters Kubernetes da comunidade.
{: shortdesc}

Para obter uma passagem rápida pelo console, consulte o [tutorial](/docs/openshift?topic=openshift-openshift_tutorial#openshift_oc_console).

Para obter mais informações sobre o console, consulte os [docs do OpenShift ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html).

<br />


## Acessando os serviços integrados do OpenShift
{: #openshift_access_oc_services}

O Red Hat OpenShift on IBM Cloud é fornecido com serviços integrados que podem ser usados para ajudar a operar seu cluster, como o console do OpenShift, o Prometheus e o Grafana. É possível acessar esses serviços usando o host local de uma [rota ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html). Os nomes de domínio de rota padrão seguem um padrão específico do cluster de `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
{:shortdesc}

É possível acessar as rotas de serviço integrado do OpenShift por meio do console do [console](#openshift_services_console) ou da [CLI](#openshift_services_cli). Você pode desejar usar o console para navegar por recursos do Kubernetes em um projeto. Usando a CLI, é possível listar recursos como rotas em projetos.

### Acessando serviços integrados do OpenShift por meio do console
{: #openshift_services_console}
1.  No console da web do OpenShift, no menu suspenso na barra de menus da plataforma de contêineres OpenShift, clique em **Console do aplicativo**.
2.  Selecione o projeto **padrão**, em seguida, na área de janela de navegação, clique em **Aplicativos > Pods**.
3.  Verifique se os pods de **roteador** estão em um status **Em execução**. O roteador funciona como o ponto de ingresso para o tráfego de rede externo. É possível usar o roteador para expor publicamente os serviços em seu cluster no endereço IP externo do roteador usando uma rota. O roteador atende na interface de rede do host público, ao contrário de seus pods de app que atendem apenas em IPs privados. O roteador executa proxy das solicitações externas para nomes do host de rota que você associa aos serviços. As solicitações são enviadas aos IPs dos pods do app que são identificados pelo serviço.
4.  Na área de janela de navegação do projeto **padrão**, clique em **Aplicativos > Implementações** e, em seguida, clique na implementação **registry-console**. Seu cluster do OpenShift é fornecido com um registro interno que pode ser usado para gerenciar imagens locais para suas implementações. Para visualizar suas imagens, clique em **Aplicativos > Rotas** e abra a URL do **Nome do host** do console do registro.
5.  Na barra de menus da plataforma de contêineres OpenShift, no menu suspenso, clique em **Console do cluster**.
6.  Na área de janela de navegação, expanda **Monitoramento**.
7.  Clique na ferramenta de monitoramento integrada que você deseja acessar, tal como **Painéis**. A rota do Grafana é aberta no formato a seguir: `https://grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.<p class="note">Na primeira vez que você acessar o nome do host poderá ser necessário se autenticar, como clicar em **Efetuar login com o OpenShift** e autorizar o acesso à sua identidade do IAM.</p>

### Acessando serviços integrados do OpenShift por meio da CLI
{: #openshift_services_cli}

1.  Na visualização **Console do aplicativo** ou **Console de serviço** no console da web do OpenShift, clique em seu perfil **IAM#user.name@email.com > Copiar comando de login** e cole o comando de login em seu terminal para autenticar.
    ```
    oc login https://c1-e.<region>.containers.cloud.ibm.com:<port> --token=<access_token>
    ```
    {: pre}
2.  Verifique se o roteador está implementado. O roteador funciona como o ponto de ingresso para o tráfego de rede externo. É possível usar o roteador para expor publicamente os serviços em seu cluster no endereço IP externo do roteador usando uma rota. O roteador atende na interface de rede do host público, ao contrário de seus pods de app que atendem apenas em IPs privados. O roteador executa proxy das solicitações externas para nomes do host de rota que você associa aos serviços. As solicitações são enviadas aos IPs dos pods do app que são identificados pelo serviço.
    ```
    oc get svc router -n default
    ```
    {: pre}

    Saída de exemplo:
    ```
    NAME      TYPE           CLUSTER-IP               EXTERNAL-IP     PORT(S)                      AGE
    router    LoadBalancer   172.21.xxx.xxx   169.xx.xxx.xxx   80:30399/TCP,443:32651/TCP                      5h
    ```
    {: screen}
2.  Obtenha o nome do host **Host/Porta** da rota de serviço que você deseja acessar. Por exemplo, você talvez deseje acessar o painel Grafana para verificar as métricas no uso de recurso de seu cluster. Os nomes de domínio de rota padrão seguem um padrão específico do cluster de `<service_name>-<namespace>.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`.
    ```
    oc get route --all-namespaces
    ```
    {: pre}

    Saída de exemplo:
    ```
    NAMESPACE                          NAME                HOST/PORT                                                                    PATH                  SERVICES            PORT               TERMINATION          WILDCARD
    default                            registry-console    registry-console-default.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                              registry-console    registry-console   passthrough          None
    kube-service-catalog               apiserver           apiserver-kube-service-catalog.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                        apiserver           secure             passthrough          None
    openshift-ansible-service-broker   asb-1338            asb-1338-openshift-ansible-service-broker.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud            asb                 1338               reencrypt            None
    openshift-console                  console             console.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                                              console             https              reencrypt/Redirect   None
    openshift-monitoring               alertmanager-main   alertmanager-main-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                alertmanager-main   web                reencrypt            None
    openshift-monitoring               grafana             grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                          grafana             https              reencrypt            None
    openshift-monitoring               prometheus-k8s      prometheus-k8s-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud                   prometheus-k8s      web                reencrypt
    ```
    {: screen}
3.  Em seu navegador da web, abra a rota que você deseja acessar, por exemplo: `https://grafana-openshift-monitoring.<cluster_name>-<random_ID>.<region>.containers.appdomain.cloud`. Na primeira vez que você acessar o nome do host poderá ser necessário se autenticar, como clicar em **Efetuar login com o OpenShift** e autorizar o acesso à sua identidade do IAM.

<br>
Agora você está no app OpenShift integrado! Por exemplo, se você estiver no Grafana, poderá consultar o uso de CPU do namespace ou de outros gráficos. Para acessar outras ferramentas integradas, abra seus nomes de host de rota.
