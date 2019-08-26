---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, rhoks, roks, rhos

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

# Armazenando dados no IBM Cloud Object Storage
{: #object_storage}

O [{{site.data.keyword.cos_full_notm}}](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage) é um armazenamento persistente e altamente disponível que você pode montar para apps que são executados em um cluster do Kubernetes usando o plug-in do {{site.data.keyword.cos_full_notm}}. O plug-in é um plug-in Flex-Volume do Kubernetes que conecta os depósitos do Cloud {{site.data.keyword.cos_short}} aos pods em seu cluster. As informações que são armazenadas com o {{site.data.keyword.cos_full_notm}} são criptografadas em trânsito e em repouso, dispersas em múltiplas localizações geográficas e acessadas por meio de HTTP usando uma API de REST.
{: shortdesc}

Para se conectar ao {{site.data.keyword.cos_full_notm}}, seu cluster requer acesso de rede pública para autenticar com o {{site.data.keyword.cloud_notm}} Identity and Access Management. Se você tiver um cluster somente privado, será possível se comunicar com o terminal em serviço privado do {{site.data.keyword.cos_full_notm}} se você instalar o plug-in versão `1.0.3` ou mais recente e configurar sua instância de serviço do {{site.data.keyword.cos_full_notm}} para autenticação HMAC. Se você não desejar usar a autenticação HMAC, deverá abrir todo o tráfego de rede de saída na porta 443 para que o plug-in funcione corretamente em um cluster privado.
{: important}

Com a versão 1.0.5, o plug-in do {{site.data.keyword.cos_full_notm}} é renomeado de `ibmcloud-object-storage-plugin` para `ibm-object-storage-plugin`. Para instalar a nova versão do plug-in, deve-se [desinstalar a instalação do gráfico do Helm antigo](#remove_cos_plugin) e [reinstalar o gráfico do Helm com a nova versão de plug-in do {{site.data.keyword.cos_full_notm}}](#install_cos).
{: note}

Com a versão 1.0.8, o gráfico do Helm do plug-in do {{site.data.keyword.cos_full_notm}} agora está disponível no repositório do Helm `ibm-charts`. Certifique-se de buscar a versão mais recente do gráfico do Helm por meio desse repositório. Para incluir o repositório, execute `helm repo add ibm-charts https://icr.io/helm/ibm-charts`.
{: note}

## Criando a sua instância de serviço de armazenamento de objeto
{: #create_cos_service}

Antes de poder começar a usar o armazenamento de objeto em seu cluster, deve-se fornecer uma instância de serviço do {{site.data.keyword.cos_full_notm}} em sua conta.
{: shortdesc}

O plug-in do {{site.data.keyword.cos_full_notm}} está configurado para funcionar com qualquer terminal de API s3. Por exemplo, você pode desejar usar um servidor Cloud Object Storage local, como o [Minio](https://cloud.ibm.com/kubernetes/solutions/helm-charts/ibm-charts/ibm-minio-objectstore) ou conectar-se a um terminal de API s3 que você configurou em um provedor em nuvem diferente em vez de usar uma instância de serviço do {{site.data.keyword.cos_full_notm}}.

Siga estas etapas para criar uma instância de serviço do {{site.data.keyword.cos_full_notm}}. Se você planeja usar um servidor Cloud Object Storage local ou um terminal de API s3 diferente, consulte a documentação do provedor para configurar sua instância do Cloud Object Storage.

1. Implementar uma instância de serviço do  {{site.data.keyword.cos_full_notm}}.
   1.  Abra a [{{site.data.keyword.cos_full_notm}} página do catálogo](https://cloud.ibm.com/catalog/services/cloud-object-storage).
   2.  Insira um nome para a sua instância de serviço (como `cos-backup`) e selecione o mesmo grupo de recursos em que seu cluster está. Para visualizar o grupo de recursos do seu cluster, execute `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>`.   
   3.  Revise as [opções de plano ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api) para obter informações de precificação e selecionar um plano.
   4.  Clique em **Criar**. A página de detalhes do serviço é aberta.
2. {: #service_credentials}Recupere as credenciais de serviço do {{site.data.keyword.cos_full_notm}}.
   1.  Na navegação na página de detalhes do serviço, clique em **Credenciais de serviço**.
   2.  Clique em **Nova credencial**. Uma caixa de diálogo é exibida.
   3.  Insira um nome para suas credenciais.
   4.  Na lista suspensa **Função**, selecione `Writer` ou `Manager`. Quando você seleciona `Reader`, não é possível usar as credenciais para criar buckets no {{site.data.keyword.cos_full_notm}} e gravar dados nele.
   5.  Opcional: em **Incluir parâmetros de configuração sequenciais (opcional)**, insira `{"HMAC":true}` para criar credenciais adicionais do HMAC para o serviço {{site.data.keyword.cos_full_notm}}. A autenticação HMAC inclui uma camada extra de segurança para a autenticação OAuth2, evitando o uso indevido de tokens OAuth2 expirados ou criados aleatoriamente. **Importante**: se você tiver um cluster somente privado sem acesso público, será necessário usar a autenticação HMAC para que seja possível acessar o serviço {{site.data.keyword.cos_full_notm}} por meio da rede privada.
   6.  Clique em **Incluir**. Suas novas credenciais são listadas na tabela **Credenciais de serviço**.
   7.  Clique em **Visualizar credenciais**.
   8.  Anote o **apikey** para usar tokens OAuth2 para autenticar com o serviço {{site.data.keyword.cos_full_notm}}. Para autenticação do HMAC, na seção **cos_hmac_keys**, anote o **access_key_id** e o **secret_access_key**.
3. [Armazene suas credenciais de serviço em um segredo do Kubernetes dentro do cluster](#create_cos_secret) para ativar o acesso à sua instância de serviço do {{site.data.keyword.cos_full_notm}}.

## Criando um segredo para as credenciais de serviço de armazenamento de objeto
{: #create_cos_secret}

Para acessar sua instância de serviço do {{site.data.keyword.cos_full_notm}} para ler e gravar dados, deve-se armazenar com segurança as credenciais de serviço em um segredo do Kubernetes. O plug-in do {{site.data.keyword.cos_full_notm}} usa essas credenciais para cada operação de leitura ou gravação em seu bucket.
{: shortdesc}

Siga estas etapas para criar um segredo do Kubernetes para as credenciais de uma instância de serviço do {{site.data.keyword.cos_full_notm}}. Se você planeja usar um servidor Cloud Object Storage local ou um terminal de API s3 diferente, crie um segredo do Kubernetes com as credenciais apropriadas.

Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Recupere o **apikey** ou o **access_key_id** e o **secret_access_key** de suas credenciais de serviço do [{{site.data.keyword.cos_full_notm}}](#service_credentials).

2. Obtenha o **GUID** de sua instância de serviço do {{site.data.keyword.cos_full_notm}}.
   ```
   ibmcloud resource service-instance <service_name> | grep GUID
   ```
   {: pre}

3. Crie um segredo do Kubernetes para armazenar suas credenciais de serviço. Ao criar seu segredo, todos os valores serão codificados automaticamente para base64.

   **Exemplo para usar a chave API:**
   ```
   oc create secret generic cos-write-access --type=ibm/ibmc-s3fs --from-literal=api-key=<api_key> --from-literal=service-instance-id=<service_instance_guid>
   ```
   {: pre}

   **Exemplo para a autenticação HMAC:**
   ```
   oc create secret generic cos-write-access --type=ibm/ibmc-s3fs --from-literal=access-key=<access_key_ID> --from-literal=secret-key=<secret_access_key>    
   ```
   {: pre}

   <table>
   <caption>Entendendo os componentes do comando</caption>
   <thead>
   <th colspan=2>Entendendo os componentes do comando<img src="images/idea.png" alt="Idea icon"/></th>
   </thead>
   <tbody>
   <tr>
   <td><code>api-key</code></td>
   <td>Insira a chave API que você recuperou de suas credenciais de serviço do {{site.data.keyword.cos_full_notm}} anteriormente. Se desejar usar a autenticação HMAC, especifique <code>access-key</code> e <code>secret-key</code>.  </td>
   </tr>
   <tr>
   <td><code>access-key</code></td>
   <td>Insira o ID da chave de acesso que você recuperou de suas credenciais de serviço do {{site.data.keyword.cos_full_notm}} anteriormente. Se você desejar usar a autenticação OAuth2, especifique a <code>api-key</code> como alternativa.  </td>
   </tr>
   <tr>
   <td><code>secret-key</code></td>
   <td>Insira a chave de acesso secreta que você recuperou de suas credenciais de serviço do {{site.data.keyword.cos_full_notm}} anteriormente. Se você desejar usar a autenticação OAuth2, especifique a <code>api-key</code> como alternativa.</td>
   </tr>
   <tr>
   <td><code>service-instance-id</code></td>
   <td>Insira o GUID de sua instância de serviço do {{site.data.keyword.cos_full_notm}} que você recuperou anteriormente. </td>
   </tr>
   </tbody>
   </table>

4. Verifique se o segredo foi criado em seu namespace.
   ```
   oc get secret
   ```
   {: pre}

5. [Instale o plug-in do {{site.data.keyword.cos_full_notm}}](#install_cos) ou, se você já tiver instalado o plug-in, [decida sobre a configuração]( #configure_cos) para o seu bucket do {{site.data.keyword.cos_full_notm}}.

## Instalando o plug-in do IBM Cloud Object Storage
{: #install_cos}

Instale o plug-in do {{site.data.keyword.cos_full_notm}} com um gráfico Helm para configurar classes de armazenamento predefinidas para o {{site.data.keyword.cos_full_notm}}. É possível usar essas classes de armazenamento para criar um PVC para provisionar o {{site.data.keyword.cos_full_notm}} para seus apps.
{: shortdesc}

Procurando instruções sobre como atualizar ou remover o plug-in do {{site.data.keyword.cos_full_notm}}? Consulte [Atualizando o plug-in](#update_cos_plugin) e [Removendo o plug-in](#remove_cos_plugin).
{: tip}

Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Certifique-se de que o nó do trabalhador aplique a correção mais recente para sua versão secundária.
   1. Liste a versão de correção atual de seus nós do trabalhador.
      ```
      ibmcloud oc workers --cluster <cluster_name_or_ID>
      ```
      {: pre}

      Saída de exemplo:
      ```
      OK
      ID                                                  Public IP        Private IP     Machine Type           State    Status   Zone    Version
      kube-dal10-crb1a23b456789ac1b20b2nc1e12b345ab-w26   169.xx.xxx.xxx    10.xxx.xx.xxx   b3c.4x16.encrypted     normal   Ready    dal10   1.13.8_1523*
      ```
      {: screen}

      Se o nó do trabalhador não aplicar a versão de correção mais recente, você verá um asterisco (`*`) na coluna **Versão** da saída da CLI.

   2. Revise o [log de mudanças de versão](/docs/containers?topic=containers-changelog#changelog) para localizar as mudanças incluídas na versão de correção mais recente.

   3. Aplique a versão de correção mais recente recarregando seu nó do trabalhador. Siga as instruções no [comando ibmcloud oc worker-reload](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) para reagendar normalmente quaisquer pods em execução em seu nó do trabalhador antes de recarregar seu nó do trabalhador. Observe que durante o recarregamento, a máquina do nó do trabalhador será atualizada com a imagem mais recente e os dados serão excluídos se não forem [armazenados fora do nó do trabalhador](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).

2.  Escolha se você deseja instalar o plug-in do {{site.data.keyword.cos_full_notm}} com ou sem o servidor do Helm, o Tiller. Em seguida, [siga as instruções](/docs/containers?topic=containers-helm#public_helm_install) para instalar o cliente do Helm em sua máquina local e, opcionalmente, o Tiller com uma conta de serviço em seu cluster. **Nota**: se você usa o Windows, deve-se instalar o Tiller.

3. Se você desejar instalar o plug-in com o Tiller, verifique se o Tiller está instalado com uma conta de serviço.
   ```
   oc get serviceaccount -n kube-system tiller
   ```
   {: pre}

   Saída de exemplo:
   ```
   NAME SECRETS AGE tiller 1 2m
   ```
   {: screen}

4. Inclua o repositório do Helm do {{site.data.keyword.cloud_notm}} em seu cluster.
   ```
   helm repo add ibm-charts https://icr.io/helm/ibm-charts
   ```
   {: pre}

4. Atualize o repositório Helm para recuperar a versão mais recente de todos os gráficos Helm nesse repositório.
   ```
   helm repo update
   ```
   {: pre}

5. Faça download dos gráficos Helm e descompacte os gráficos em seu diretório atual.
   ```
   helm fetch --untar ibm-charts/ibm-object-storage-plugin
   ```
   {: pre}

7. Se você usar o OS X ou uma distribuição Linux, instale o plug-in do Helm do {{site.data.keyword.cos_full_notm}} `ibmc`. O plug-in é usado para recuperar automaticamente o local do cluster e para configurar o terminal de API para os buckets do {{site.data.keyword.cos_full_notm}} em suas classes de armazenamento. Se você usar o Windows como seu sistema operacional, continue com a próxima etapa.
   1. Instale o plug-in Helm.
      ```
      helm plugin install ./ibm-object-storage-plugin/helm-ibmc
      ```
      {: pre}

      Saída de exemplo:
      ```
      Plug-in instalado: ibmc
      ```
      {: screen}

      Se você vir o erro `Error: plugin already exists`, remova o plug-in do Helm `ibmc` executando `rm -rf ~/.helm/plugins/helm-ibmc`.
      {: tip}

   2. Verifique se o plug-in `ibmc` está instalado com êxito.
      ```
      helm ibmc --help
      ```
      {: pre}

      Saída de exemplo:
      ```
      Install or upgrade Helm charts in IBM K8S Service(IKS) and IBM Cloud Private(ICP)

      Available Commands:
         helm ibmc install [CHART][flags]                      Install a Helm chart
         helm ibmc upgrade [RELEASE][CHART] [flags]            Upgrade the release to a new version of the Helm chart
         helm ibmc template [CHART][flags] [--apply|--delete]  Install/uninstall a Helm chart without tiller

      Available Flags:
         -h, --help                    (Optional) This text.
         -u, --update                  (Optional) Update this plugin to the latest version

      Example Usage:
         With Tiller:
             Install:   helm ibmc install ibm-charts/ibm-object-storage-plugin --name ibm-object-storage-plugin
         Without Tiller:
             Install:   helm ibmc template ibm-charts/ibm-object-storage-plugin --apply
             Dry-run:   helm ibmc template ibm-charts/ibm-object-storage-plugin
             Uninstall: helm ibmc template ibm-charts/ibm-object-storage-plugin --delete

      Nota:
         1. É sempre recomendado instalar a versão mais recente do gráfico ibm-object-storage-plugin.
         2. É sempre recomendado ter o cliente 'oc' atualizado.
      ```
      {: screen}

      Se a saída mostrar o erro `Error: fork/exec /home/iksadmin/.helm/plugins/helm-ibmc/ibmc.sh: permission denied`, execute `chmod 755 ~/.helm/plugins/helm-ibmc/ibmc.sh`. Em seguida, reexecute `helm ibmc -- help`.
      {: tip}

8. Opcional: limite o plug-in do {{site.data.keyword.cos_full_notm}} para acessar somente os segredos do Kubernetes que contêm as credenciais de serviço do {{site.data.keyword.cos_full_notm}}. Por padrão, o plug-in está autorizado a acessar todos os segredos do Kubernetes em seu cluster.
   1. [Crie sua instância de serviço {{site.data.keyword.cos_full_notm}}](#create_cos_service).
   2. [Armazene suas credenciais de serviço do {{site.data.keyword.cos_full_notm}} em um segredo do Kubernetes](#create_cos_secret).
   3. Navegue para o diretório `templates` e liste os arquivos disponíveis.  
      ```
      cd ibm-object-storage-plugin/templates && ls
      ```
      {: pre}

   4. Abra o arquivo `provisioner-sa.yaml` e procure a definição `ibmcloud-object-storage-secret-reader` de `ClusterRole`.
   6. Inclua o nome do segredo que você criou anteriormente para a lista de segredos que o plug-in está autorizado a acessar na seção `resourceNames`.
      ```
      kind: ClusterRole
      apiVersion: rbac.authorization.k8s.io/v1beta1
      metadata:
        name: ibmcloud-object-storage-secret-reader
      rules:
      - apiGroups: [""]
        resources: ["secrets"]
        resourceNames: ["<secret_name1>","<secret_name2>"]
        verbs: ["get"]
      ```
      {: codeblock}
   7. Salve as suas mudanças.

9. Instale o plug-in do {{site.data.keyword.cos_full_notm}}. Quando você instala o plug-in, as classes de armazenamento predefinidas são incluídas em seu cluster.

   - **Para OS X e Linux:**
     - Se você ignorou a etapa anterior, instale sem uma limitação para segredos específicos do Kubernetes.</br>
       **Sem tiller**:
       ```
       helm ibmc template ibm-charts/ibm-object-storage-plugin --apply
       ```
       {: pre}

       **Com tiller**:
       ```
       helm ibmc install ibm-charts/ibm-object-storage-plugin --name ibm-object-storage-plugin
       ```
       {: pre}

     - Se você concluiu a etapa anterior, instale com uma limitação para segredos específicos do Kubernetes.</br>
       **Sem tiller**:
       ```
       cd ../..
       helm ibmc template./ibm-object-storage-plugin --apply
       ```
       {: pre}

       **Com tiller**:
       ```
       cd ../..
       helm ibmc install./ibm-object-storage-plugin --name ibm-object-storage-plugin
       ```
       {: pre}

   - **Para o Windows:**
     1. Recupere a zona em que o cluster está implementado e armazene a zona em uma variável de ambiente.
        ```
        export DC_NAME=$(oc get cm cluster-info -n kube-system -o jsonpath='{.data.cluster-config\.json}' | grep datacenter | awk -F ': ' '{print $2}' | sed 's/\"//g' |sed 's/,//g')
        ```
        {: pre}

     2. Verifique se a variável de ambiente está configurada.
        ```
        printenv
        ```
        {: pre}

     3. Instale o gráfico Helm.
        - Se você ignorou a etapa anterior, instale sem uma limitação para segredos específicos do Kubernetes.</br>
          ```
          helm install ibm-charts/ibm-object-storage-plugin --name ibm-object-storage-plugin
          ```
          {: pre}

        - Se você concluiu a etapa anterior, instale com uma limitação para segredos específicos do Kubernetes.</br>
          ```
          cd ../..
          helm install ./ibm-object-storage-plugin --name ibm-object-storage-plugin
          ```
          {: pre}

   Saída de exemplo para instalação sem o Tiller:
   ```
   Rendering the Helm chart templates...
   DC: dal10
   Chart: ibm-charts/ibm-object-storage-plugin
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-cold-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-cold-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-flex-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-flex-perf-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-flex-perf-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-flex-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-standard-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-standard-perf-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-standard-perf-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-standard-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-vault-cross-region.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/ibmc-s3fs-vault-regional.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/flex-driver-sa.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/provisioner-sa.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/flex-driver.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/tests/check-driver-install.yaml
   wrote object-storage-templates/ibm-object-storage-plugin/templates/provisioner.yaml
   Installing the Helm chart...
   serviceaccount/ibmcloud-object-storage-driver created
   daemonset.apps/ibmcloud-object-storage-driver created
   storageclass.storage.k8s.io/ibmc-s3fs-cold-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-cold-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-flex-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-flex-perf-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-flex-perf-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-flex-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-standard-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-standard-perf-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-standard-perf-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-standard-regional created
   storageclass.storage.k8s.io/ibmc-s3fs-vault-cross-region created
   storageclass.storage.k8s.io/ibmc-s3fs-vault-regional created
   serviceaccount/ibmcloud-object-storage-plugin created
   clusterrole.rbac.authorization.k8s.io/ibmcloud-object-storage-plugin created
   clusterrole.rbac.authorization.k8s.io/ibmcloud-object-storage-secret-reader created
   clusterrolebinding.rbac.authorization.k8s.io/ibmcloud-object-storage-plugin created
   clusterrolebinding.rbac.authorization.k8s.io/ibmcloud-object-storage-secret-reader created
   deployment.apps/ibmcloud-object-storage-plugin created
   pod/ibmcloud-object-storage-driver-test created
   ```
   {: screen}

10. Verifique se o plug-in está instalado corretamente.
    ```
    oc get pod -n default -o wide | grep object
    ```
    {: pre}

    Saída de exemplo:
    ```
    ibmcloud-object-storage-driver-9n8g8                              1/1       Running   0          2m
   ibmcloud-object-storage-plugin-7c774d484b-pcnnx                   1/1       Running   0          2m
    ```
    {: screen}

    A instalação é bem-sucedida quando você vê um pod `ibmcloud-object-storage-plugin` e um ou mais pods `ibmcloud-storage-object-storage-driver`. O número de pods `ibmcloud-object-storage-driver` é igual ao número de nós do trabalhador em seu cluster. Todos os pods devem estar em um estado `Running` para que o plug-in funcione de forma adequada. Se os pods falharem, execute `oc describe pod -n kube-system <pod_name>` para localizar a causa raiz para a falha.

11. Verifique se as classes de armazenamento foram criadas com êxito.
    ```
    oc get storageclass | grep s3
    ```
    {: pre}

    Saída de exemplo:
    ```
    ibmc-s3fs-cold-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-cold-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-cross-region       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-regional           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-cross-region        ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-cross-region   ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-regional       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-regional            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-cross-region           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-regional               ibm.io/ibmc-s3fs   8m
    ```
    {: screen}

12. Repita as etapas para todos os clusters nos quais você deseja acessar os buckets do {{site.data.keyword.cos_full_notm}}.

### Atualizando o plug-in do IBM Cloud Object Storage
{: #update_cos_plugin}

É possível fazer upgrade do plug-in do {{site.data.keyword.cos_full_notm}} existente para a versão mais recente.
{: shortdesc}

1. Se você instalou anteriormente a versão 1.0.4 ou anterior do gráfico do Helm que é denominado `ibmcloud-object-storage-plugin`, remova essa instalação do Helm do seu cluster. Em seguida, reinstale o gráfico do Helm.
   1. Verifique se a versão antiga do gráfico do Helm do {{site.data.keyword.cos_full_notm}} está instalada em seu cluster.  
      ```
      helm ls | grep ibmcloud-object-storage-plugin
      ```
      {: pre}

      Saída de exemplo:
      ```
      ibmcloud-object-storage-plugin	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-object-storage-plugin-1.0.4	default
      ```
      {: screen}

   2. Se você tiver a versão 1.0.4 ou anterior do gráfico do Helm que é denominado `ibmcloud-object-storage-plugin`, remova o gráfico do Helm do seu cluster. Se você tiver a versão 1.0.5 ou mais recente do gráfico do Helm que é denominado `ibm-object-storage-storage-plugin`, continue com a Etapa 2.
      ```
      helm delete --purge ibmcloud-object-storage-plugin
      ```
      {: pre}

   3. Siga as etapas em [Instalando o plug-in do {{site.data.keyword.cos_full_notm}}](#install_cos) para instalar a versão mais recente do plug-in do {{site.data.keyword.cos_full_notm}}.

2. Atualize o repositório do Helm do {{site.data.keyword.cloud_notm}} para recuperar a versão mais recente de todos os gráficos do Helm nesse repositório.
   ```
   helm repo update
   ```
   {: pre}

3. Se você usar o OS X ou uma distribuição Linux, atualize o plug-in do Helm do {{site.data.keyword.cos_full_notm}} `ibmc` para a versão mais recente.
   ```
   helm ibmc -- update
   ```
   {: pre}

4. Faça download do gráfico do Helm do {{site.data.keyword.cos_full_notm}} mais recente em sua máquina local e extraia o pacote para revisar o arquivo `release.md` para localizar as informações de liberação mais recentes.
   ```
   helm fetch --untar ibm-charts/ibm-object-storage-plugin
   ```
   {: pre}

5. Faça upgrade do plug-in. </br>
   **Sem tiller**:
   ```
   helm ibmc template ibm-charts/ibm-object-storage-plugin --update
   ```
   {: pre}

   **Com tiller**:
   1. Localize o nome da instalação do gráfico do Helm.
      ```
      helm ls | grep ibm-object-storage-plugin
      ```
      {: pre}

      Saída de exemplo:
      ```
      <helm_chart_name> 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibm-object-storage-plugin-1.0.5	default
      ```
      {: screen}

   2. Faça upgrade do gráfico do Helm do {{site.data.keyword.cos_full_notm}} para a versão mais recente.
      ```   
      helm ibmc upgrade <helm_chart_name> ibm-charts/ibm-object-storage-plugin --force --recreate-pods -f
      ```
      {: pre}

6. Verifique se o `ibmcloud-object-storage-plugin` foi submetido a upgrade com êxito.  
   ```
   oc rollout status deployment/ibmcloud-object-storage-plugin -n kube-system
   ```
   {: pre}

   O upgrade do plug-in é bem-sucedido quando você vê `deployment "ibmcloud-object-storage-plugin" successfully rolled out` em sua saída da CLI.

7. Verifique se o `ibmcloud-object-storage-driver` foi submetido a upgrade com êxito.
   ```
   oc rollout status ds/ibmcloud-object-storage-driver -n kube-system
   ```
   {: pre}

   O upgrade é bem-sucedido quando você vê `daemon set "ibmcloud-object-storage-driver" successfully rolled out` em sua saída da CLI.

8. Verifique se os pods do {{site.data.keyword.cos_full_notm}} estão em um estado `Running`.
   ```
   oc get pods -n kube-system -o wide | grep object-storage
   ```
   {: pre}


### Removendo o plug-in do IBM Cloud Object Storage
{: #remove_cos_plugin}

Se você não desejar provisionar nem usar o {{site.data.keyword.cos_full_notm}} em seu cluster, será possível desinstalar o plug-in.
{: shortdesc}

A remoção do plug-in não remove os PVCs, PVs ou dados existentes. Quando você remove o plug-in, todos os pods e conjuntos de daemon relacionados são removidos do cluster. Não é possível provisionar um novo {{site.data.keyword.cos_full_notm}} para seu cluster ou usar PVCs e PVs existentes depois de remover o plug-in, a menos que você configure seu app para usar a API do {{site.data.keyword.cos_full_notm}} diretamente.
{: important}

Antes de iniciar:

- [Destinar sua CLI para o cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).
- Certifique-se de que você não tenha nenhum PVC ou PV no cluster que use o {{site.data.keyword.cos_full_notm}}. Para listar todos os pods que montam uma PVC específica, execute `oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"`.

Para remover o plug-in:

1. Remova o plug-in de seu cluster. </br>
   **Com tiller**:
   1. Localize o nome da instalação do gráfico do Helm.
      ```
      helm ls | grep object-storage-plugin
      ```
      {: pre}

      Saída de exemplo:
      ```
      <helm_chart_name> 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-object-storage-plugin-1.0.0	default
      ```
      {: screen}

   2. Exclua o plug-in do {{site.data.keyword.cos_full_notm}} removendo o gráfico Helm.
      ```
      helm delete --purge <helm_chart_name>
      ```
      {: pre}

   **Sem tiller**:
   ```
   helm ibmc template ibm-charts/ibm-object-storage-plugin --delete
   ```
   {: pre}

2. Verifique se os pods  {{site.data.keyword.cos_full_notm}}  são removidos.
   ```
   oc get pod -n kube-system | grep object-storage
   ```
   {: pre}

   A remoção dos pods será bem-sucedida se nenhum pod for exibido na saída da CLI.

3. Verifique se as classes de armazenamento foram removidas.
   ```
   oc get storageclasses | grep s3
   ```
   {: pre}

   A remoção das classes de armazenamento será bem-sucedida se nenhuma classe de armazenamento for exibida na saída da CLI.

4. Se você usar o OS X ou uma distribuição Linux, remova o plug-in do Helm `ibmc`. Se você usar o Windows, esta etapa não será necessária.
   1. Remova o plug-in  ` ibmc ` .
      ```
      rm -rf ~/.helm/plugins/helm-ibmc
      ```
      {: pre}

   2. Verifique se o plug-in `ibmc` foi removido.
      ```
      helm plugin list
      ```
      {: pre}

      Saída de exemplo:
     ```
     NAME	VERSION	DESCRIPTION
     ```
     {: screen}

     O plug-in `ibmc` foi removido com êxito se o plug-in `ibmc` não estiver listado em sua saída da CLI.


## Decidindo sobre a configuração de armazenamento de objeto
{: #configure_cos}

O {{site.data.keyword.containerlong_notm}} fornece classes de armazenamento predefinidas que podem ser usadas para criar buckets com uma configuração específica.
{: shortdesc}

1. Liste as classes de armazenamento disponíveis no  {{site.data.keyword.containerlong_notm}}.
   ```
   oc get storageclasses | grep s3
   ```
   {: pre}

   Saída de exemplo:
   ```
   ibmc-s3fs-cold-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-cold-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-cross-region            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-cross-region       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-perf-regional           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-flex-regional                ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-cross-region        ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-cross-region   ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-perf-regional       ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-standard-regional            ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-cross-region           ibm.io/ibmc-s3fs   8m
   ibmc-s3fs-vault-regional               ibm.io/ibmc-s3fs   8m
   ```
   {: screen}

2. Escolha uma classe de armazenamento que se ajuste aos seus requisitos de acesso a dados. A classe de armazenamento determina a [precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api) para capacidade de armazenamento, operações de leitura e gravação e largura da banda de saída para um bucket. A opção certa para você é baseada na frequência com que os dados são lidos e gravados em sua instância de serviço.
   - **Padrão**: essa opção é usada para dados quentes que são acessados frequentemente. Casos de uso comuns são apps da web ou móveis.
   - **Área segura**: essa opção é usada para cargas de trabalho ou dados frios que são acessados infrequentemente, como uma vez por mês ou menos. Os casos de uso comum são archives, retenção de dados de curto prazo, preservação de ativo digital, substituição de fita e recuperação de desastre.
   - **Frio**: essa opção é usada para dados frios que são raramente acessados (a cada 90 dias ou menos) ou dados inativos. Os casos de uso comum são archives, backups de longo prazo, dados históricos que você mantém para conformidade ou cargas de trabalho e apps que são raramente acessados.
   - **Flex**: essa opção é usada para cargas de trabalho e dados que não seguem um padrão de uso específico ou que são muito grandes para determinar ou prever um padrão de uso. **Dica:** verifique este [blog ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2017/03/interconnect-2017-changing-rules-storage/) para saber como a classe de armazenamento Flex funciona em comparação com as camadas de armazenamento tradicionais.   

3. Decida sobre o nível de resiliência para os dados que estão armazenados em seu bucket.
   - **Região cruzada**: com essa opção, seus dados são armazenados em três regiões dentro de uma localização geográfica para a maior disponibilidade. Se você tiver cargas de trabalho que estão distribuídas entre regiões, as solicitações serão roteadas para o terminal regional mais próximo. O terminal de API para a localização geográfica é configurado automaticamente pelo plug-in do Helm `ibmc` que você instalou anteriormente com base no local em que o seu cluster está. Por exemplo, se seu cluster está em `US South`, suas classes de armazenamento são configuradas para usar o terminal de API `US GEO` para seus buckets. Para obter mais informações, consulte [Regiões e terminais](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).  
   - **Regional**: com essa opção, seus dados são replicados em múltiplas zonas dentro de uma região. Se tiver cargas de trabalho que estão localizadas na mesma região, você verá latência inferior e melhor desempenho do que em uma configuração entre regiões. O terminal regional é configurado automaticamente pelo plug-in do Helm `ibm` que você instalou anteriormente com base no local em que seu cluster está. Por exemplo, se seu cluster está em `US South`, suas classes de armazenamento foram configuradas para usar `US South` como o terminal regional para seus buckets. Para obter mais informações, consulte [Regiões e terminais](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints).

4. Revise a configuração detalhada do bucket do {{site.data.keyword.cos_full_notm}} para uma classe de armazenamento.
   ```
   oc describe storageclass <storageclass_name>
   ```
   {: pre}

   Saída de exemplo:
   ```
   Name:                  ibmc-s3fs-standard-cross-region
   IsDefaultClass:        No
   Annotations:           <none>
   Provisioner:           ibm.io/ibmc-s3fs
   Parameters:            ibm.io/chunk-size-mb=16,ibm.io/curl-debug=false,ibm.io/debug-level=warn,ibm.io/iam-endpoint=https://iam.bluemix.net,ibm.io/kernel-cache=true,ibm.io/multireq-max=20,ibm.io/object-store-endpoint=https://s3-api.dal-us-geo.objectstorage.service.networklayer.com,ibm.io/object-store-storage-class=us-standard,ibm.io/parallel-count=2,ibm.io/s3fs-fuse-retry-count=5,ibm.io/stat-cache-size=100000,ibm.io/tls-cipher-suite=AESGCM
   AllowVolumeExpansion:  <unset>
   MountOptions:          <none>
   ReclaimPolicy:         Delete
   VolumeBindingMode:     Immediate
   Events:                <none>
   ```
   {: screen}

   <table>
   <caption>Entendendo os detalhes da classe de armazenamento</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Ícone de ideia"/> entendendo os componentes de arquivo do YAML</th>
   </thead>
   <tbody>
   <tr>
   <td><code>ibm.io/chunk-size-mb</code></td>
   <td>O tamanho de uma parte de dados que é lida ou gravada no {{site.data.keyword.cos_full_notm}} em megabytes. As classes de armazenamento com <code>perf</code> em seu nome são configuradas com 52 megabytes. As classes de armazenamento sem <code>perf</code> em seu nome usam chunks de 16 megabytes. Por exemplo, se você desejar ler um arquivo que tem `1 GB`, o plug-in lerá esse arquivo em múltiplos chunks de 16 ou 52 megabytes. </td>
   </tr>
   <tr>
   <td><code>ibm.io/curl-debug</code></td>
   <td>Ative a criação de log de solicitações que são enviadas para a instância de serviço do {{site.data.keyword.cos_full_notm}}. Se ativado, os logs são enviados para `syslog` e é possível [encaminhar os logs para um servidor de criação de log externo](/docs/containers?topic=containers-health#logging). Por padrão, todas as classes de armazenamento são configuradas como <strong>false</strong> para desativar esse recurso de criação de log. </td>
   </tr>
   <tr>
   <td><code>ibm.io/debug-level</code></td>
   <td>O nível de criação de log que é configurado pelo plug-in do {{site.data.keyword.cos_full_notm}}. Todas as classes de armazenamento são configuradas com o nível de criação de log <strong>WARN</strong>. </td>
   </tr>
   <tr>
   <td><code>ibm.io/iam-endpoint</code></td>
   <td>O terminal de API do {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). </td>
   </tr>
   <tr>
   <td><code>ibm.io/kernel-cache</code></td>
   <td>Ative ou desative o cache do buffer do kernel para o ponto de montagem do volume. Se ativado, os dados que são lidos no {{site.data.keyword.cos_full_notm}} são armazenados no cache de kernel para assegurar acesso rápido de leitura a seus dados. Se desativado, os dados não são armazenados em cache e sempre lidos no {{site.data.keyword.cos_full_notm}}. O cache de kernel é ativado para classes de armazenamento <code>standard</code> e <code>flex</code> e desativado para classes de armazenamento <code>cold</code> e <code>vault</code>. </td>
   </tr>
   <tr>
   <td><code>ibm.io/multireq-max</code></td>
   <td>O número máximo de solicitações paralelas que podem ser enviadas para a instância de serviço do {{site.data.keyword.cos_full_notm}} para listar arquivos em um único diretório. Todas as classes de armazenamento são configuradas com um máximo de 20 solicitações paralelas.  </td>
   </tr>
   <tr>
   <td><code>ibm.io/object-store-endpoint</code></td>
   <td>O terminal de API a ser usado para acessar o bucket em sua instância de serviço do {{site.data.keyword.cos_full_notm}}. O terminal é configurado automaticamente com base na região de seu cluster. **Nota**: se você desejar acessar um depósito existente que está localizado em uma região diferente daquela em que seu cluster está, deve-se criar uma [classe de armazenamento customizada](/docs/containers?topic=containers-kube_concepts#customized_storageclass) e usar o terminal de API para seu depósito.</td>
   </tr>
   <tr>
   <td><code>ibm.io/object-store-storage-class</code></td>
   <td>O nome da classe de armazenamento. </td>
   </tr>
   <tr>
   <td><code>ibm.io/parallel-count</code></td>
   <td>O número máximo de solicitações paralelas que podem ser enviadas para a instância de serviço do {{site.data.keyword.cos_full_notm}} para uma única operação de leitura ou gravação. As classes de armazenamento com <code>perf</code> em seu nome são configuradas com um máximo de 20 solicitações paralelas. As classes de armazenamento sem <code>perf</code> são configuradas com duas solicitações paralelas por padrão.  </td>
   </tr>
   <tr>
   <td><code>ibm.io/s3fs-fuse-retry-count</code></td>
   <td>O número máximo de novas tentativas para uma operação de leitura ou gravação antes que a operação seja considerada malsucedida. Todas as classes de armazenamento são configuradas com um máximo de cinco novas tentativas.  </td>
   </tr>
   <tr>
   <td><code>ibm.io/stat-cache-size</code></td>
   <td>O número máximo de registros que são mantidos no cache de metadados do {{site.data.keyword.cos_full_notm}}. Cada registro pode ocupar até 0,5 kilobytes. Todas as classes de armazenamento configuram o número máximo de registros como 100000 por padrão. </td>
   </tr>
   <tr>
   <td><code>ibm.io/tls-cipher-suite</code></td>
   <td>O conjunto de cifras do TLS que deve ser usado quando uma conexão com o {{site.data.keyword.cos_full_notm}} é estabelecida por meio do terminal HTTPS. O valor para o conjunto de cifras deve seguir o [formato OpenSSL ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). Se os nós do trabalhador executarem um sistema operacional Ubuntu, as classes de armazenamento serão configuradas para usar o conjunto de cifras <strong><code>AESGCM</code></strong> por padrão. Para nós do trabalhador que executam um sistema operacional Red Hat, o conjunto de cifras <strong><code>ecdhe_rsa_rsa_aes_128_gcm_sha_256</code></strong> é usado por padrão.    </td>
   </tr>
   </tbody>
   </table>

   Para obter mais informações sobre cada classe de armazenamento, consulte a [referência de classe de armazenamento](#cos_storageclass_reference). Se você desejar mudar qualquer um dos valores pré-configurados, crie sua própria [classe de armazenamento customizada](/docs/containers?topic=containers-kube_concepts#customized_storageclass).
   {: tip}

5. Decida sobre um nome para o seu bucket. O nome de um bucket deve ser exclusivo no {{site.data.keyword.cos_full_notm}}. Também é possível criar automaticamente um nome para seu bucket pelo plug-in do {{site.data.keyword.cos_full_notm}}. Para organizar dados em um bucket, é possível criar subdiretórios.

   A classe de armazenamento que você escolheu anteriormente determina a precificação para o depósito inteiro. Não é possível definir classes de armazenamento diferentes para subdiretórios. Se você deseja armazenar dados com diferentes requisitos de acesso, considere a criação de múltiplos buckets usando múltiplos PVCs.
   {: note}

6. Escolha se você deseja manter seus dados e o bucket após o cluster ou a solicitação de volume persistente (PVC) ser excluída. Quando você exclui o PVC, o PV é sempre excluído. É possível escolher se você deseja também excluir automaticamente os dados e o bucket ao excluir o PVC. Sua instância de serviço do {{site.data.keyword.cos_full_notm}} é independente da política de retenção que você seleciona para seus dados e nunca é removida ao excluir um PVC.

Agora que decidiu sobre a configuração desejada, você está pronto para [criar um PVC](#add_cos) para provisionar o {{site.data.keyword.cos_full_notm}}.

## Incluindo armazenamento de objeto em apps
{: #add_cos}

Crie uma solicitação de volume persistente (PVC) para provisionar o {{site.data.keyword.cos_full_notm}} para seu cluster.
{: shortdesc}

Dependendo das configurações que você escolher em seu PVC, é possível provisionar o {{site.data.keyword.cos_full_notm}} das maneiras a seguir:
- [Fornecimento dinâmico](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning): quando você cria o PVC, o volume persistente (PV) correspondente e o bucket em sua instância de serviço do {{site.data.keyword.cos_full_notm}} são criados automaticamente.
- [Fornecimento estático](/docs/containers?topic=containers-kube_concepts#static_provisioning): é possível referenciar um bucket existente em sua instância de serviço do {{site.data.keyword.cos_full_notm}} em seu PVC. Quando você cria o PVC, somente o PV correspondente é criado e vinculado automaticamente ao seu bucket existente no {{site.data.keyword.cos_full_notm}}.

Antes de iniciar:
- [ Crie e prepare sua  {{site.data.keyword.cos_full_notm}}  instância de serviço ](#create_cos_service).
- [Crie um segredo para armazenar suas credenciais de serviço do {{site.data.keyword.cos_full_notm}}](#create_cos_secret).
- [ Decida sobre a configuração para seu  {{site.data.keyword.cos_full_notm}} ](#configure_cos).

Para incluir o  {{site.data.keyword.cos_full_notm}}  em seu cluster:

1. Crie um arquivo de configuração para definir a sua solicitação de volume persistente (PVC).
   ```
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: <pvc_name>
     namespace: <namespace>
     annotations:
       ibm.io/auto-create-bucket: "<true_or_false>"
       ibm.io/auto-delete-bucket: "<true_or_false>"
       ibm.io/bucket: "<bucket_name>"
       ibm.io/object-path: "<bucket_subdirectory>"
       ibm.io/secret-name: "<secret_name>"
       ibm.io/endpoint: "https://<s3fs_service_endpoint>"
   spec:
     accessModes:
       - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi # Enter a fictitious value
     storageClassName: <storage_class>
   ```
   {: codeblock}

   <table>
   <caption>Entendendo os componentes de arquivo YAML</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Ícone de ideia"/> entendendo os componentes de arquivo do YAML</th>
   </thead>
   <tbody>
   <tr>
   <td><code>metadata.name</code></td>
   <td>Insira o nome do PVC.</td>
   </tr>
   <tr>
   <td><code>metadata.namespace</code></td>
   <td>Insira o namespace no qual você deseja criar o PVC. O PVC deve ser criado no mesmo namespace no qual você criou o segredo do Kubernetes para as suas credenciais de serviço do {{site.data.keyword.cos_full_notm}} e no local em que deseja executar o seu pod. </td>
   </tr>
   <tr>
   <td><code>ibm.io/auto-create-bucket</code></td>
   <td>Escolha entre as opções a seguir: <ul><li><strong>true</strong>: quando você cria o PVC, o PV e o bucket em sua instância de serviço do {{site.data.keyword.cos_full_notm}} são criados automaticamente. Escolha essa opção para criar um novo bucket em sua instância de serviço do {{site.data.keyword.cos_full_notm}}. </li><li><strong>false</strong>: escolha essa opção se você desejar acessar dados em um bucket existente. Quando você cria o PVC, o PV é criado e vinculado automaticamente ao bucket especificado em <code>ibm.io/bucket</code>.</td>
   </tr>
   <tr>
   <td><code> ibm.io/auto-delete-bucket </code></td>
   <td>Escolha entre as opções a seguir: <ul><li><strong>true</strong>: seus dados, o bucket e o PV são removidos automaticamente quando você exclui o PVC. A instância de serviço do {{site.data.keyword.cos_full_notm}} permanece e não é excluída. Se você escolhe configurar essa opção como <strong>true</strong>, deve-se configurar <code>ibm.io/auto-create-bucket: true</code> e <code>ibm.io/bucket: ""</code> para que seu bucket seja criado automaticamente com um nome com o formato <code>tmp-s3fs-xxxx</code>. </li><li><strong>false</strong>: quando você exclui o PVC, o PV é excluído automaticamente, mas os seus dados e o bucket em sua instância de serviço do {{site.data.keyword.cos_full_notm}} permanecem. Para acessar seus dados, deve-se criar um novo PVC com o nome de seu bucket existente. </li></ul>
   <tr>
   <td><code> ibm.io/bucket </code></td>
   <td>Escolha entre as opções a seguir: <ul><li>Se <code>ibm.io/auto-create-bucket</code> estiver configurado como <strong>true</strong>: insira o nome do bucket que você deseja criar no {{site.data.keyword.cos_full_notm}}. Se, além disso, <code>ibm.io/auto-delete-bucket</code> está configurado como <strong>true</strong>, deve-se deixar esse campo em branco para designar automaticamente seu bucket a um nome com o formato <code>tmp-s3fs-xxxx</code>. O nome deve ser exclusivo no  {{site.data.keyword.cos_full_notm}}. </li><li>Se <code>ibm.io/auto-create-bucket</code> estiver configurado como <strong>false</strong>: insira o nome do bucket existente que você deseja acessar no cluster. </li></ul> </td>
   </tr>
   <tr>
   <td><code> ibm.io/object-path </code></td>
   <td>Opcional: insira o nome do subdiretório existente no bucket que você deseja montar. Use essa opção se desejar montar somente um subdiretório e não o bucket inteiro. Para montar um subdiretório, deve-se configurar <code>ibm.io/auto-create-bucket: "false"</code> e fornecer o nome do bucket em <code>ibm.io/bucket</code>. </li></ul> </td>
   </tr>
   <tr>
   <td><code> ibm.io/secret-name </code></td>
   <td>Insira o nome do segredo que contém as credenciais do {{site.data.keyword.cos_full_notm}} que você criou anteriormente. </td>
   </tr>
   <tr>
  <td><code>ibm.io/endpoint</code></td>
  <td>Se você criou sua instância de serviço do {{site.data.keyword.cos_full_notm}} em um local que seja diferente de seu cluster, insira o terminal em serviço privado ou público de sua instância de serviço do {{site.data.keyword.cos_full_notm}} que deseja usar. Para obter uma visão geral de terminais em serviço disponíveis, consulte [Informações adicionais do terminal](/docs/services/cloud-object-storage?topic=cloud-object-storage-advanced-endpoints). Por padrão, o plug-in do Helm <code>ibmc</code> recupera automaticamente o local do cluster e cria as classes de armazenamento usando o terminal em serviço privado do {{site.data.keyword.cos_full_notm}} que corresponde ao seu local do cluster. Se o cluster estiver em uma das zonas de cidade metropolitana, como `dal10`, o terminal em serviço privado do {{site.data.keyword.cos_full_notm}} para a cidade metropolitana, neste caso, Dallas, será usado. Para verificar se o terminal em serviço em suas classes de armazenamento corresponde ao terminal em serviço da sua instância de serviço, execute `oc describe storageclass <storageclassname>`. Certifique-se de inserir seu terminal em serviço no formato `https://<s3fs_private_service_endpoint>` para os terminais em serviço privado ou `http://<s3fs_public_service_endpoint>` para os terminais em serviço público. Se o terminal em serviço em sua classe de armazenamento corresponder ao terminal em serviço de sua instância de serviço do {{site.data.keyword.cos_full_notm}}, não inclua a opção <code>ibm.io/endpoint</code> em seu arquivo YAML da PVC. </td>
  </tr>
   <tr>
   <td><code>resources.requests.storage</code></td>
   <td>Um tamanho fictício para o seu bucket do {{site.data.keyword.cos_full_notm}} em gigabytes. O tamanho é necessário para o Kubernetes, mas não é respeitado no {{site.data.keyword.cos_full_notm}}. É possível inserir qualquer tamanho que desejar. O espaço real que você usa no {{site.data.keyword.cos_full_notm}} pode ser diferente e é faturado com base na [tabela de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api). </td>
   </tr>
   <tr>
   <td><code> spec.storageClassName </code></td>
   <td>Escolha entre as opções a seguir: <ul><li>Se <code>ibm.io/auto-create-bucket</code> estiver configurado como <strong>true</strong>: insira a classe de armazenamento que você deseja usar para seu novo bucket. </li><li>Se <code>ibm.io/auto-create-bucket</code> estiver configurado como <strong>false</strong>: insira a classe de armazenamento que você usou para criar seu bucket existente. </br></br>Se você criou manualmente o depósito em sua instância de serviço do {{site.data.keyword.cos_full_notm}} ou não consegue se lembrar da classe de armazenamento usada, localize sua instância de serviço no painel do {{site.data.keyword.Bluemix}} e revise a <strong>Classe</strong> e o <strong>Local</strong> de seu depósito existente. Em seguida, use a  [ classe de armazenamento ](#cos_storageclass_reference) apropriada. <p class="note">O terminal de API do {{site.data.keyword.cos_full_notm}} que está configurado em sua classe de armazenamento se baseia na região em que seu cluster está. Se você desejar acessar um bucket que está localizado em uma região diferente daquela em que seu cluster está, deve-se criar uma [classe de armazenamento customizada](/docs/containers?topic=containers-kube_concepts#customized_storageclass) e usar o terminal de API apropriado para seu bucket.</p></li></ul>  </td>
   </tr>
   </tbody>
   </table>

2. Crie o PVC.
   ```
   oc apply -f filepath/pvc.yaml
   ```
   {: pre}

3. Verifique se o PVC foi criado e ligado ao PV.
   ```
   oc get pvc
   ```
   {: pre}

   Saída de exemplo:
   ```
   NAME                  STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                     AGE
   s3fs-test-pvc         Bound     pvc-b38b30f9-1234-11e8-ad2b-t910456jbe12   8Gi        RWO            ibmc-s3fs-standard-cross-region  1h
   ```
   {: screen}

4. Opcional: se você planejar acessar seus dados com um usuário não raiz ou arquivos incluídos em um depósito do {{site.data.keyword.cos_full_notm}} existente usando o console ou a API diretamente, certifique-se de que os [arquivos tenham a permissão correta](/docs/containers?topic=containers-cs_troubleshoot_storage#cos_nonroot_access) designada para que seu app possa ler e atualizar com êxito os arquivos, conforme necessário.

4.  {: #cos_app_volume_mount}Para montar o PV em sua implementação, crie um arquivo de configuração `.yaml` e especifique o PVC que liga o PV.

    ```
    apiVersion: apps/v1 kind: Deployment metadata: name: <deployment_name> labels: app: <deployment_label> spec: selector: matchLabels: app: <app_name> template: metadata: labels: app: <app_name> spec: containers:
          - image: <image_name>
            name: <container_name>
            securityContext:
              runAsUser: <non_root_user>
              fsGroup: <non_root_user> #only applicable for clusters that run Kubernetes version 1.13 or later
            volumeMounts:
            - name: <volume_name>
              mountPath: /<file_path>
          volumes:
          - name: <volume_name>
            persistentVolumeClaim:
              claimName: <pvc_name>
    ```
    {: codeblock}

    <table>
    <caption>Entendendo os componentes de arquivo YAML</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Ícone de ideia"/> entendendo os componentes de arquivo do YAML</th>
    </thead>
    <tbody>
        <tr>
    <td><code> metadata.labels.app </code></td>
    <td>Um rótulo para a implementação.</td>
      </tr>
      <tr>
        <td><code>spec.selector.matchLabels.app</code> <br/> <code> spec.template.metadata.labels.app </code></td>
        <td>Um rótulo para o seu app.</td>
      </tr>
    <tr>
    <td><code> template.metadata.labels.app </code></td>
    <td>Um rótulo para a implementação.</td>
      </tr>
    <tr>
    <td><code> spec.containers.image </code></td>
    <td>O nome da imagem que você deseja usar. Para listar as imagens disponíveis em sua conta do {{site.data.keyword.registryshort_notm}}, execute `ibmcloud cr image-list`.</td>
    </tr>
    <tr>
    <td><code> spec.containers.name </code></td>
    <td>O nome do contêiner que você deseja implementar em seu cluster.</td>
    </tr>
    <tr>
    <td><code> spec.containers.securityContext.runAsUser </code></td>
    <td>Opcional: para executar o aplicativo com um usuário não raiz em um cluster que execute o Kubernetes versão 1.12 ou anterior, especifique o [contexto de segurança ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/) para seu pod definindo o usuário não raiz sem configurar o `fsGroup` no YAML de sua implementação ao mesmo tempo. Configurar o `fsGroup` aciona o plug-in do {{site.data.keyword.cos_full_notm}} para atualizar as permissões de grupo para todos os arquivos em um depósito quando o pod é implementado. A atualização das permissões é uma operação de gravação e afeta o desempenho. Dependendo de quantos arquivos você tem, a atualização das permissões pode evitar que seu pod fique ativo e entre em um estado <code>Running</code>. </br></br>Se tiver um cluster que execute o Kubernetes versão 1.13 ou mais recente e o plug-in do {{site.data.keyword.cloud_notm}} Object Storage versão 1.0.4 ou mais recente, será possível mudar o proprietário do ponto de montagem s3fs. Para isso, especifique o contexto de segurança configurando `runAsUser` e `fsGroup` para o mesmo ID do usuário não raiz que deseja que possua o ponto de montagem s3fs. Se esses dois valores não corresponderem, o ponto de montagem será automaticamente de propriedade do usuário `root`.  </td>
    </tr>
    <tr>
    <td><code> spec.containers.volumeMounts.mountPath </code></td>
    <td>O caminho absoluto do diretório no qual o volume está montado dentro do contêiner. Se você desejar compartilhar um volume entre apps diferentes, será possível especificar [subcaminhos do volume ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath) para cada um de seus apps.</td>
    </tr>
    <tr>
    <td><code> spec.containers.volumeMounts.name </code></td>
    <td>O nome do volume a ser montado no pod.</td>
    </tr>
    <tr>
    <td><code> volumes.name </code></td>
    <td>O nome do volume a ser montado no pod. Geralmente, esse nome é o mesmo que <code>volumeMounts/name</code>.</td>
    </tr>
    <tr>
    <td><code> volumes.persistentVolumeClaim.claimName </code></td>
    <td>O nome do PVC que liga o PV que você deseja usar. </td>
    </tr>
    </tbody></table>

5.  Crie a implementação.
     ```
     oc apply -f <local_yaml_path>
     ```
     {: pre}

6.  Verifique se o PV foi montado com êxito.

     ```
     oc describe deployment <deployment_name>
     ```
     {: pre}

     O ponto de montagem está no campo **Montagens de volume** e o volume está no campo **Volumes**.

     ```
      Volume Mounts:
          /var/run/secrets/kubernetes.io/serviceaccount from default-token-tqp61 (ro)
          /volumemount from myvol (rw)
     ...
     Volumes:
      myvol:
        Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
        ClaimName: mypvc
        ReadOnly: false
     ```
     {: screen}

7. Verifique se é possível gravar dados em sua instância de serviço do {{site.data.keyword.cos_full_notm}}.
   1. Efetue login no pod que monta seu PV.
      ```
      oc exec <pod_name> -it bash
      ```
      {: pre}

   2. Navegue para o caminho de montagem do volume que você definiu em sua implementação de app.
   3. Crie um arquivo de texto.
      ```
      echo "This is a test" > test.txt
      ```
      {: pre}

   4. No painel do {{site.data.keyword.Bluemix}}, navegue para a instância de serviço do {{site.data.keyword.cos_full_notm}}.
   5. No menu, selecione  ** Buckets **.
   6. Abra seu bucket e verifique se é possível ver o `test.txt` que você criou.


## Usando o armazenamento de objetos em um conjunto stateful
{: #cos_statefulset}

Se você tiver um app stateful, como um banco de dados, será possível criar conjuntos stateful que usam o {{site.data.keyword.cos_full_notm}} para armazenar os dados de seu app. Como alternativa, é possível usar um banco de dados como um serviço do {{site.data.keyword.cloud_notm}} (tal como o {{site.data.keyword.cloudant_short_notm}}) e armazenar seus dados na nuvem.
{: shortdesc}

Antes de iniciar:
- [ Crie e prepare sua  {{site.data.keyword.cos_full_notm}}  instância de serviço ](#create_cos_service).
- [Crie um segredo para armazenar suas credenciais de serviço do {{site.data.keyword.cos_full_notm}}](#create_cos_secret).
- [ Decida sobre a configuração para seu  {{site.data.keyword.cos_full_notm}} ](#configure_cos).

Para implementar um conjunto stateful que usa armazenamento de objetos:

1. Crie um arquivo de configuração para seu conjunto stateful e o serviço usado para expor o conjunto stateful. Os exemplos a seguir mostram como implementar o NGINX como um conjunto stateful com três réplicas. Cada réplica com um depósito separado ou compartilhando o mesmo depósito.

   **Exemplo para criar um conjunto stateful com três réplicas, com cada réplica utilizando um depósito separado**:
   ```
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-v01
     namespace: default
     labels:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   spec:
     ports:
     - port: 80
       name: web
     clusterIP: None
     selector:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   ---
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: web-v01
     namespace: default
   spec:
     selector:
       matchLabels:
         app: nginx-v01 # must match spec.template.metadata.labels in stateful set YAML and metadata.labels in service YAML
     serviceName: "nginx-v01"
     replicas: 3 
     template:
       metadata:
         labels:
           app: nginx-v01 # must match spec.selector.matchLabels in stateful set YAML and metadata.labels in service YAML
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: nginx
           image: k8s.gcr.io/nginx-slim:0.8
           ports:
           - containerPort: 80
             name: web
           volumeMounts:
           - name: mypvc
             mountPath: /usr/share/nginx/html
     volumeClaimTemplates:
     - metadata:
         name: mypvc
         annotations:
           ibm.io/auto-create-bucket: "true"
           ibm.io/auto-delete-bucket: "true"
           ibm.io/bucket: ""
           ibm.io/secret-name: mysecret 
           volume.beta.kubernetes.io/storage-class: ibmc-s3fs-standard-perf-cross-region 
           volume.beta.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
       spec:
         accessModes: [ "ReadWriteOnce" ]
         storageClassName: "ibmc-s3fs-standard-perf-cross-region"
         resources:
           requests:
             storage: 1Gi
   ```
   {: codeblock}

   **Exemplo para criar um conjunto stateful com três réplicas que compartilham o mesmo depósito `mybucket`**:
   ```
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-v01
     namespace: default
     labels:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   spec:
     ports:
     - port: 80
       name: web
     clusterIP: None
     selector:
       app: nginx-v01 # must match spec.template.metadata.labels and spec.selector.matchLabels in stateful set YAML
   --- 
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: web-v01
     namespace: default
   spec:
     selector:
       matchLabels:
         app: nginx-v01 # must match spec.template.metadata.labels in stateful set YAML and metadata.labels in service YAML
     serviceName: "nginx-v01"
     replicas: 3 
     template:
       metadata:
         labels:
           app: nginx-v01 # must match spec.selector.matchLabels in stateful set YAML and metadata.labels in service YAML
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: nginx
           image: k8s.gcr.io/nginx-slim:0.8
           ports:
           - containerPort: 80
             name: web
           volumeMounts:
           - name: mypvc
             mountPath: /usr/share/nginx/html
     volumeClaimTemplates:
     - metadata:
         name: mypvc
         annotations:
           ibm.io/auto-create-bucket: "false"
           ibm.io/auto-delete-bucket: "false"
           ibm.io/bucket: mybucket
           ibm.io/secret-name: mysecret
           volume.beta.kubernetes.io/storage-class: ibmc-s3fs-standard-perf-cross-region 
           volume.beta.kubernetes.io/storage-provisioner: ibm.io/ibmc-s3fs
       spec:
         accessModes: [ "ReadOnlyMany" ]
         storageClassName: "ibmc-s3fs-standard-perf-cross-region"
         resources:
           requests:
             storage: 1Gi
   ```
   {: codeblock}


   <table>
    <caption>Entendendo os componentes de arquivo YAML do conjunto stateful</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Ícone Ideia"/> Entendendo os componentes de arquivo YAML do conjunto stateful</th>
    </thead>
    <tbody>
    <tr>
    <td style="text-align:left"><code>metadata.name</code></td>
    <td style="text-align:left">Insira um nome para seu conjunto stateful. O nome inserido é usado para criar o nome para seu PVC no formato: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code> spec.serviceName </code></td>
    <td style="text-align:left">Insira o nome do serviço que deseja usar para expor o conjunto stateful. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code> spec.replicas </code></td>
    <td style="text-align:left">Insira o número de réplicas para seu conjunto stateful. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code> spec.selector.matchLabels </code></td>
    <td style="text-align:left">Insira todos os rótulos que deseja incluir no conjunto stateful e no PVC. Os rótulos incluídos no <code>volumeClaimTemplates</code> de seu conjunto stateful não são reconhecidos pelo Kubernetes. Em vez disso, deve-se definir esses rótulos na seção <code>spec.selector.matchLabels</code> e <code>spec.template.metadata.labels</code> de seu YAML do conjunto stateful. Para certificar-se de que todas as réplicas do conjunto stateful estejam incluídas no balanceamento de carga de seu serviço, inclua o mesmo rótulo que você usou na seção <code>spec.selector</code> de seu YAML de serviço. </td>
    </tr>
    <tr>
    <td style="text-align:left"><code> spec.template.metadata.labels </code></td>
    <td style="text-align:left">Insira os mesmos rótulos que você incluiu na seção <code>spec.selector.matchLabels</code> de seu YAML do conjunto stateful. </td>
    </tr>
    <tr>
    <td><code>spec.template.spec.</code></br><code>terminationGracePeriodSeconds</code></td>
    <td>Insira o número de segundos para fornecer ao <code>kubelet</code> para finalizar normalmente o pod que executa sua réplica do conjunto stateful. Para obter mais informações, veja [Excluir pods ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/tasks/run-application/force-delete-stateful-set-pod/#delete-pods). </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.</code></br><code>metadata.name</code></td>
    <td style="text-align:left">Insira um nome para seu volume. Use o mesmo nome definido na seção <code>spec.containers.volumeMount.name</code>. O nome inserido aqui é usado para criar o nome para seu PVC no formato: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
    </tr>
    <tr>
    <td><code>spec.volumeClaimTemplates.metadata</code></br><code>annotions.ibm.io/auto-create-bucket</code></td>
    <td>Escolha entre as opções a seguir: <ul><li><strong>true: </strong>escolha essa opção para criar automaticamente um bucket para cada réplica do conjunto stateful. </li><li><strong>false: </strong>escolha essa opção se você desejar compartilhar um bucket existente em suas réplicas do conjunto stateful. Certifique-se de definir o nome do bucket na seção <code>spec.volumeClaimTemplates.metadata.annotions.ibm.io/bucket</code> de seu YAML do conjunto stateful.</li></ul></td>
    </tr>
    <tr>
    <td><code>spec.volumeClaimTemplates.metadata</code></br><code>annotions.ibm.io/auto-delete-bucket</code></td>
    <td>Escolha entre as opções a seguir: <ul><li><strong>true: </strong>seus dados, o bucket e o PV são removidos automaticamente quando você exclui o PVC. A instância de serviço do {{site.data.keyword.cos_full_notm}} permanece e não é excluída. Se você escolhe configurar essa opção como true, deve-se configurar <code>ibm.io/auto-create-bucket: true</code> e <code>ibm.io/bucket: ""</code> para que seu bucket seja criado automaticamente com um nome com o formato <code>tmp-s3fs-xxxx</code>. </li><li><strong>false</strong>: quando você exclui o PVC, o PV é excluído automaticamente, mas os seus dados e o bucket em sua instância de serviço do {{site.data.keyword.cos_full_notm}} permanecem. Para acessar seus dados, deve-se criar um novo PVC com o nome de seu bucket existente.</li></ul></td>
    </tr>
    <tr>
    <td><code>spec.volumeClaimTemplates.metadata</code></br><code>annotions.ibm.io/bucket</code></td>
    <td>Escolha entre as opções a seguir: <ul><li><strong>Se <code>ibm.io/auto-create-bucket</code> estiver configurado como true</strong>: insira o nome do bucket que você deseja criar no {{site.data.keyword.cos_full_notm}}. Se, além disso, <code>ibm.io/auto-delete-bucket</code> está configurado como <strong>true</strong>, deve-se deixar esse campo em branco para designar automaticamente seu bucket a um nome com o formato tmp-s3fs-xxxx. O nome deve ser exclusivo no  {{site.data.keyword.cos_full_notm}}.</li><li><strong>Se <code>ibm.io/auto-create-bucket</code> estiver configurado como false</strong>: insira o nome do bucket existente que você deseja acessar no cluster.</li></ul></td>
    </tr>
    <tr>
    <td><code>spec.volumeClaimTemplates.metadata</code></br><code>annotions.ibm.io/secret-name</code></td>
    <td>Insira o nome do segredo que contém as credenciais do {{site.data.keyword.cos_full_notm}} que você criou anteriormente.</td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.metadata.</code></br><code>annotations.volume.beta.</code></br><code>kubernetes.io/storage-class</code></td>
    <td style="text-align:left">Insira a classe de armazenamento que deseja usar. Escolha entre as opções a seguir: <ul><li><strong>Se <code>ibm.io/auto-create-bucket</code> estiver configurado como true</strong>: insira a classe de armazenamento que você deseja usar para seu novo bucket.</li><li><strong>Se <code>ibm.io/auto-create-bucket</code> estiver configurado como false</strong>: insira a classe de armazenamento que você usou para criar seu bucket existente. </li></ul></br>  Para listar classes de armazenamento existentes, execute <code>oc get storageclasses | grep s3</code>. Se você não especificar uma classe de armazenamento, o PVC será criado com a classe de armazenamento padrão configurada em seu cluster. Certifique-se de que a classe de armazenamento padrão use o provisionador <code>ibm.io/ibmc-s3fs</code> para que seu conjunto stateful seja provisionado com armazenamento de objetos.</td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.</code></br><code>spec.storageClassName</code></td>
    <td>Insira a mesma classe de armazenamento que você inseriu na seção <code>spec.volumeClaimTemplates.metadata.annotations.volume.beta.kubernetes.io/storage-class</code> de seu YAML do conjunto stateful.  </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.</code></br><code>resource.requests.storage</code></td>
    <td>Insira um tamanho fictício para o seu bucket do {{site.data.keyword.cos_full_notm}} em gigabytes. O tamanho é necessário para o Kubernetes, mas não é respeitado no {{site.data.keyword.cos_full_notm}}. É possível inserir qualquer tamanho que desejar. O espaço real que você usa no {{site.data.keyword.cos_full_notm}} pode ser diferente e é faturado com base na [tabela de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api).</td>
    </tr>
    </tbody></table>


## Fazendo backup e restaurando dados
{: #cos_backup_restore}

O {{site.data.keyword.cos_full_notm}} é configurado para fornecer alta durabilidade para seus dados para que eles sejam protegidos contra perda. É possível localizar o SLA nos [termos de serviço do {{site.data.keyword.cos_full_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7857-03).
{: shortdesc}

O {{site.data.keyword.cos_full_notm}} não fornece um histórico de versão para seus dados. Se você precisa manter e acessar versões mais antigas de seus dados, deve-se configurar seu app para gerenciar o histórico de dados ou implementar soluções de backup alternativas. Por exemplo, você pode desejar armazenar seus dados do {{site.data.keyword.cos_full_notm}} em seu banco de dados no local ou usar fitas para arquivar seus dados.
{: note}

## Referência de classe de armazenamento
{: #cos_storageclass_reference}

### Padrão
{: #standard}

<table>
<caption>Classe de armazenamento de objeto: padrão</caption>
<thead>
<th>Características</th>
<th>Configuração</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-s3fs-standard-cross-region</code></br><code>ibmc-s3fs-standard-perf-cross-region</code></br><code>ibmc-s3fs-standard-regional</code></br><code>ibmc-s3fs-standard-perf-regional</code></td>
</tr>
<tr>
<td>Terminal de resiliência padrão</td>
<td>O terminal de resiliência é configurado automaticamente com base no local em que seu cluster está. Para obter mais informações, consulte [Regiões e terminais](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Tamanho do chunk</td>
<td>Classes de armazenamento sem `perf`: 16 MB</br>Classes de armazenamento com `perf`: 52 MB</td>
</tr>
<tr>
<td>Cache do Kernel</td>
<td>Ativado</td>
</tr>
<tr>
<td>Faturamento</td>
<td>Mensal</td>
</tr>
<tr>
<td>Precificação</td>
<td>[Precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api)</td>
</tr>
</tbody>
</table>

### Segurança
{: #Vault}

<table>
<caption>Classe de armazenamento de objeto: área segura</caption>
<thead>
<th>Características</th>
<th>Configuração</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-s3fs-vault-cross-region</code></br><code>ibmc-s3fs-vault-regional</code></td>
</tr>
<tr>
<td>Terminal de resiliência padrão</td>
<td>O terminal de resiliência é configurado automaticamente com base no local em que seu cluster está. Para obter mais informações, consulte [Regiões e terminais](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Tamanho do chunk</td>
<td>16 MB</td>
</tr>
<tr>
<td>Cache do Kernel</td>
<td>Desativado</td>
</tr>
<tr>
<td>Faturamento</td>
<td>Mensal</td>
</tr>
<tr>
<td>Precificação</td>
<td>[Precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api)</td>
</tr>
</tbody>
</table>

### Frio
{: #cold}

<table>
<caption>Classe de armazenamento de objeto: cold</caption>
<thead>
<th>Características</th>
<th>Configuração</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-s3fs-flex-cross-region</code></br><code>ibmc-s3fs-flex-perf-cross-region</code></br><code>ibmc-s3fs-flex-regional</code></br><code>ibmc-s3fs-flex-perf-regional</code></td>
</tr>
<tr>
<td>Terminal de resiliência padrão</td>
<td>O terminal de resiliência é configurado automaticamente com base no local em que seu cluster está. Para obter mais informações, consulte [Regiões e terminais](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Tamanho do chunk</td>
<td>16 MB</td>
</tr>
<tr>
<td>Cache do Kernel</td>
<td>Desativado</td>
</tr>
<tr>
<td>Faturamento</td>
<td>Mensal</td>
</tr>
<tr>
<td>Precificação</td>
<td>[Precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api)</td>
</tr>
</tbody>
</table>

### Flexível
{: #flex}

<table>
<caption>Classe de armazenamento de objeto: flex</caption>
<thead>
<th>Características</th>
<th>Configuração</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-s3fs-cold-cross-region</code></br><code>ibmc-s3fs-flex-perf-cross-region</code></br><code>ibmc-s3fs-cold-regional</code></br><code>ibmc-s3fs-flex-perf-regional</code></td>
</tr>
<tr>
<td>Terminal de resiliência padrão</td>
<td>O terminal de resiliência é configurado automaticamente com base no local em que seu cluster está. Para obter mais informações, consulte [Regiões e terminais](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints). </td>
</tr>
<tr>
<td>Tamanho do chunk</td>
<td>Classes de armazenamento sem `perf`: 16 MB</br>Classes de armazenamento com `perf`: 52 MB</td>
</tr>
<tr>
<td>Cache do Kernel</td>
<td>Ativado</td>
</tr>
<tr>
<td>Faturamento</td>
<td>Mensal</td>
</tr>
<tr>
<td>Precificação</td>
<td>[Precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api)</td>
</tr>
</tbody>
</table>


