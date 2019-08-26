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

# Armazenando dados no IBM Cloud Block Storage clássico
{: #block_storage}

O {{site.data.keyword.cloud_notm}} Block Storage é um armazenamento iSCSI persistente de alto desempenho que é possível incluir em seus apps usando volumes persistentes do Kubernetes (PVs). É possível escolher entre camadas de armazenamento predefinidas com tamanhos de GB e IOPS que atendam aos requisitos de suas cargas de trabalho. Para descobrir se o {{site.data.keyword.cloud_notm}} Block Storage é a opção de armazenamento correta para você, consulte [Escolhendo uma solução de armazenamento](/docs/containers?topic=containers-storage_planning#choose_storage_solution). Para obter mais informações sobre precificação, consulte [Faturamento](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#billing).
{: shortdesc}

O {{site.data.keyword.cloud_notm}} Block Storage está disponível somente para clusters padrão. Se o seu cluster não puder acessar a rede pública, como um cluster privado atrás de um firewall ou um cluster com apenas o terminal em serviço privado ativado, certifique-se de ter instalado o plug-in do {{site.data.keyword.cloud_notm}} Block Storage versão 1.3.0 ou mais recente para se conectar à sua instância de armazenamento de bloco por meio da rede privada. As instâncias de armazenamento de bloco são específicas para uma única zona. Se você tiver um cluster de múltiplas zonas, considere as [opções de armazenamento persistente multizona](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).
{: important}

## Instalando o plug-in do {{site.data.keyword.cloud_notm}} Block Storage em seu cluster
{: #install_block}

Instale o plug-in do {{site.data.keyword.cloud_notm}} Block Storage com um gráfico Helm para configurar classes de armazenamento predefinidas para armazenamento de bloco. É possível usar essas classes de armazenamento para criar um PVC para provisionar armazenamento de bloco para seus apps.
{: shortdesc}

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

1.  [Siga as instruções](/docs/containers?topic=containers-helm#public_helm_install) para instalar o cliente Helm em sua máquina local e instale o servidor Helm (Tiller) com uma conta de serviço em seu cluster.

    A instalação do Tiller do servidor Helm requer uma conexão de rede pública com o Google Container Registry público. Se o seu cluster não puder acessar a rede pública, como um cluster privado atrás de um firewall ou um cluster com apenas o terminal em serviço privado que está ativado, você poderá optar por [enviar por pull a imagem do Tiller para a máquina local e enviar por push a imagem para seu namespace no {{site.data.keyword.registryshort_notm}}](/docs/containers?topic=containers-helm#private_local_tiller) ou [instalar o gráfico do Helm sem usar o Tiller](/docs/containers?topic=containers-helm#private_install_without_tiller).
    {: note}

2.  Verifique se o tiller está instalado com uma conta de serviço.

    ```
    oc get serviceaccount -n kube-system tiller
    ```
    {: pre}

    Saída de exemplo:

    ```
    NAME SECRETS AGE tiller 1 2m
    ```
    {: screen}

3. Inclua o repositório do gráfico Helm do {{site.data.keyword.cloud_notm}} no cluster no qual você deseja usar o plug-in do {{site.data.keyword.cloud_notm}} Block Storage.
   ```
   helm repo add iks-charts https://icr.io/helm/iks-charts
   ```
   {: pre}

4. Atualize o repositório Helm para recuperar a versão mais recente de todos os gráficos Helm nesse repositório.
   ```
   helm repo update
   ```
   {: pre}

5. Instale o {{site.data.keyword.cloud_notm}} Block Storage plug-in. Quando você instala o plug-in, classes de armazenamento de bloco predefinidas são incluídas no cluster.
   ```
   helm install iks-charts/ibmcloud-block-storage-plugin
   ```
   {: pre}

   Saída de exemplo:
   ```
   NAME:   bald-olm
   LAST DEPLOYED: Wed Apr 18 10:02:55 2018
   NAMESPACE: default
   STATUS: DEPLOYED

   RESOURCES:
   ==> v1beta1/DaemonSet
   NAME                           DESIRED  CURRENT  READY  UP-TO-DATE  AVAILABLE  NODE SELECTOR  AGE
   ibmcloud-block-storage-driver  0        0        0      0           0          <none>         0s

   ==> v1beta1/Deployment
   NAME                           DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
   ibmcloud-block-storage-plugin  1        0        0           0          0s

   ==> v1/StorageClass
   NAME                      PROVISIONER        AGE
   ibmc-block-bronze         ibm.io/ibmc-block  0s
   ibmc-block-custom         ibm.io/ibmc-block  0s
   ibmc-block-gold           ibm.io/ibmc-block  0s
   ibmc-block-retain-bronze  ibm.io/ibmc-block  0s
   ibmc-block-retain-custom  ibm.io/ibmc-block  0s
   ibmc-block-retain-gold    ibm.io/ibmc-block  0s
   ibmc-block-retain-silver  ibm.io/ibmc-block  0s
   ibmc-block-silver         ibm.io/ibmc-block  0s

   ==> v1/ServiceAccount
   NAME                           SECRETS  AGE
   ibmcloud-block-storage-plugin  1        0s

   ==> v1beta1/ClusterRole
   NAME                           AGE
   ibmcloud-block-storage-plugin  0s

   ==> v1beta1/ClusterRoleBinding
   NAME                           AGE
   ibmcloud-block-storage-plugin  0s

   NOTES:
   Thank you for installing: ibmcloud-block-storage-plugin.   Your release is named: bald-olm
   ```
   {: screen}

6. Verifique se a instalação foi bem-sucedida.
   ```
   oc get pod -n kube-system | grep block
   ```
   {: pre}

   Saída de exemplo:
   ```
   ibmcloud-block-storage-driver-kh4mt                              1/1       Running   0          27d       10.118.98.19   10.118.98.19
   ibmcloud-block-storage-plugin-58c5f9dc86-pbl4t                   1/1       Running   0          14d       172.21.0.204   10.118.98.19
   ```
   {: screen}

   A instalação é bem-sucedida quando você vê um pod `ibmcloud-block-storage-plugin` e um ou mais pods `ibmcloud-block-storage-driver`. O número de pods `ibmcloud-block-storage-driver` é igual ao número de nós do trabalhador em seu cluster. Todos os pods devem estar em um estado **Executando**.

7. Verifique se as classes de armazenamento para armazenamento de bloco foram incluídas no cluster.
   ```
   oc get storageclasses | grep block
   ```
   {: pre}

   Saída de exemplo:
   ```
   ibmc-block-bronze            ibm.io/ibmc-block
   ibmc-block-custom            ibm.io/ibmc-block
   ibmc-block-gold              ibm.io/ibmc-block
   ibmc-block-retain-bronze     ibm.io/ibmc-block
   ibmc-block-retain-custom     ibm.io/ibmc-block
   ibmc-block-retain-gold       ibm.io/ibmc-block
   ibmc-block-retain-silver     ibm.io/ibmc-block
   ibmc-block-silver            ibm.io/ibmc-block
   ```
   {: screen}

8. Repita essas etapas para cada cluster no qual você deseja provisionar armazenamento de bloco.

Agora é possível continuar a [criar um PVC](#add_block) para provisionar armazenamento de bloco para seu app.


### Atualizando o plug-in do {{site.data.keyword.cloud_notm}} Block Storage
É possível fazer upgrade do plug-in existente do {{site.data.keyword.cloud_notm}} Block Storage para a versão mais recente.
{: shortdesc}

Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Atualize o repositório Helm para recuperar a versão mais recente de todos os gráficos Helm nesse repositório.
   ```
   helm repo update
   ```
   {: pre}

2. Opcional: faça download do gráfico Helm mais recente em sua máquina local. Em seguida, extraia o pacote e revise o arquivo `release.md` para localizar as informações de liberação mais recentes.
   ```
   helm fetch iks-charts/ibmcloud-block-storage-plugin
   ```
   {: pre}

3. Localize o nome do gráfico do Helm de armazenamento de bloco que você instalou em seu cluster.
   ```
   helm ls | grep ibmcloud-block-storage-plugin
   ```
   {: pre}

   Saída de exemplo:
   ```
   myhelmchart 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-block-storage-plugin-0.1.0	default
   ```
   {: screen}

4. Faça upgrade do plug-in do {{site.data.keyword.cloud_notm}} Block Storage para a versão mais recente.
   ```
   helm upgrade --force --recreate-pods <helm_chart_name>  iks-charts/ibmcloud-block-storage-plugin
   ```
   {: pre}

5. Opcional: quando você atualiza o plug-in, a classe de armazenamento `default` está desconfigurada. Se você deseja configurar a classe de armazenamento padrão para uma classe de armazenamento de sua escolha, execute o comando a seguir.
   ```
   oc patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
   ```
   {: pre}


### Removendo o plug-in do {{site.data.keyword.cloud_notm}} Block Storage
Se você não deseja provisionar e usar o {{site.data.keyword.cloud_notm}} Block Storage em seu cluster, é possível desinstalar o gráfico Helm.
{: shortdesc}

A remoção do plug-in não remove os PVCs, PVs ou dados existentes. Quando você remove o plug-in, todos os pods e conjuntos de daemon relacionados são removidos do cluster. Não é possível provisionar novo armazenamento de bloco para seu cluster ou usar PVCs e PVs de armazenamento de bloco existentes depois de remover o plug-in.
{: important}

Antes de iniciar:
- [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
- Certifique-se de que você não tenha nenhum PVC ou PV em seu cluster que use armazenamento de bloco.

Para remover o plug-in:

1. Localize o nome do gráfico do Helm de armazenamento de bloco que você instalou em seu cluster.
   ```
   helm ls | grep ibmcloud-block-storage-plugin
   ```
   {: pre}

   Saída de exemplo:
   ```
   myhelmchart 	1       	Mon Sep 18 15:31:40 2017	DEPLOYED	ibmcloud-block-storage-plugin-0.1.0	default
   ```
   {: screen}

2. Exclua o plug-in do {{site.data.keyword.cloud_notm}} Block Storage.
   ```
   helm delete <helm_chart_name>
   ```
   {: pre}

3. Verifique se os pods de armazenamento de bloco foram removidos.
   ```
   oc get pod -n kube-system | grep ibmcloud-block-storage-plugin
   ```
   {: pre}
   A remoção dos pods será bem-sucedida se nenhum pod for exibido na saída da CLI.

4. Verifique se as classes de armazenamento de bloco foram removidas.
   ```
   oc get storageclasses | grep block
   ```
   {: pre}
   A remoção das classes de armazenamento será bem-sucedida se nenhuma classe de armazenamento for exibida na saída da CLI.

<br />



## Decidindo sobre a configuração de armazenamento de bloco
{: #block_predefined_storageclass}

O {{site.data.keyword.containerlong}} fornece classes de armazenamento predefinidas para armazenamento de bloco que podem ser usadas para provisionar armazenamento de bloco com uma configuração específica.
{: shortdesc}

Cada classe de armazenamento especifica o tipo de armazenamento de bloco que você provisiona, incluindo o tamanho disponível, o IOPS, o sistema de arquivos e a política de retenção.  

Certifique-se de escolher a configuração de armazenamento com cuidado para ter capacidade suficiente para armazenar seus dados. Após você provisionar um tipo específico de armazenamento usando uma classe de armazenamento, não será possível mudar o tamanho, o tipo, o IOPS ou a política de retenção para o dispositivo de armazenamento. Se você precisar de mais armazenamento ou armazenamento com uma configuração diferente, deverá [criar uma nova instância de armazenamento e copiar os dados](/docs/containers?topic=containers-kube_concepts#update_storageclass) da instância de armazenamento antiga para a sua nova.
{: important}

1. Liste as classes de armazenamento disponíveis no  {{site.data.keyword.containerlong}}.
    ```
    oc get storageclasses | grep block
    ```
    {: pre}

    Saída de exemplo:
    ```
    $ oc get storageclasses
    NAME                         TYPE
    ibmc-block-custom            ibm.io/ibmc-block
    ibmc-block-bronze            ibm.io/ibmc-block
    ibmc-block-gold              ibm.io/ibmc-block
    ibmc-block-silver            ibm.io/ibmc-block
    ibmc-block-retain-bronze     ibm.io/ibmc-block
    ibmc-block-retain-silver     ibm.io/ibmc-block
    ibmc-block-retain-gold       ibm.io/ibmc-block
    ibmc-block-retain-custom     ibm.io/ibmc-block
    ```
    {: screen}

2. Revise a configuração de uma classe de armazenamento.
   ```
   oc describe storageclass <storageclass_name>
   ```
   {: pre}

   Para obter mais informações sobre cada classe de armazenamento, consulte a [referência de classe de armazenamento](#block_storageclass_reference). Se você não localizar o que está procurando, considere criar a sua própria classe de armazenamento customizada. Para iniciar, consulte as [amostras de classe de armazenamento customizadas](#block_custom_storageclass).
   {: tip}

3. Escolha o tipo de armazenamento de bloco que você deseja provisionar.
   - **Classes de armazenamento de bronze, prata e ouro:** essas classes de armazenamento provisionam o [Armazenamento do Endurance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance). Com o armazenamento Endurance, é possível escolher o tamanho do armazenamento em gigabytes em camadas de IOPS predefinidas.
   - **Classe de armazenamento customizado:** essa classe de armazenamento provisiona o [Armazenamento de desempenho](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provperformance). Com o armazenamento de desempenho, você tem mais controle sobre o tamanho do armazenamento e do IOPS.

4. Escolha o tamanho e o IOPS para seu armazenamento de bloco. O tamanho e o número de IOPS definem o número total de IOPS (operações de entrada/saída por segundo) que serve como um indicador de quão rápido o seu armazenamento é. Quanto mais total de IOPS o seu armazenamento tiver, mais rápido ele processará operações de leitura e gravação.
   - **Classes de armazenamento bronze, prata e ouro:** essas classes de armazenamento vêm com um número fixo de IOPS por gigabyte e são provisionadas em discos rígidos SSD. O número total de IOPS depende do tamanho do armazenamento que você escolher. É possível selecionar qualquer número inteiro de gigabyte dentro do intervalo de tamanho permitido, como 20 Gi, 256 Gi ou 11854 Gi. Para determinar o número total de IOPS, deve-se multiplicar o IOPS com o tamanho selecionado. Por exemplo, se você selecionar um tamanho de armazenamento de bloco de 1000Gi na classe de armazenamento prata que é fornecida com 4 IOPS por GB, seu armazenamento terá um total de 4.000 IOPS.  
     <table>
         <caption>Tabela de intervalos de tamanho de classe de armazenamento e IOPS por gigabyte</caption>
         <thead>
         <th>Classe de armazenamento</th>
         <th>IOPS por gigabyte</th>
         <th>Intervalo de tamanho em gigabytes</th>
         </thead>
         <tbody>
         <tr>
         <td>Bronze</td>
         <td>2 IOPS/GB</td>
         <td>20-12.000 Gi</td>
         </tr>
         <tr>
         <td>Prata</td>
         <td>4 IOPS/GB</td>
         <td>20-12.000 Gi</td>
         </tr>
         <tr>
         <td>Ouro</td>
         <td>10 IOPS/GB</td>
         <td>20 - 4.000 Gi</td>
         </tr>
         </tbody></table>
   - **Classe de armazenamento customizada:** quando você escolhe essa classe de armazenamento, tem mais controle sobre o tamanho e o IOPS desejados. Para o tamanho, é possível selecionar qualquer número inteiro de gigabyte dentro do intervalo de tamanho permitido. O tamanho que você escolher determinará o intervalo de IOPS que estará disponível para você. É possível escolher um IOPS que é um múltiplo de 100 que esteja no intervalo especificado. O IOPS que você escolhe é estático e não escala com o tamanho do armazenamento. Por exemplo, se você escolher 40 Gi com 100 IOPS, o seu IOPS total permanecerá 100. </br></br>A razão de IOPS para gigabytes também determina o tipo de disco rígido provisionado para você. Por exemplo, se você tiver 500 Gi a 100 IOPS, a sua razão de IOPS para gigabyte será 0,2. O armazenamento com uma razão menor ou igual a 0,3 é provisionado em discos rígidos SATA. Se a sua razão for maior que 0,3, o armazenamento será provisionado em discos rígidos SSD.
     <table>
         <caption>Tabela de intervalos de tamanho de classe de armazenamento customizado e IOPS</caption>
         <thead>
         <th>Intervalo de tamanho em gigabytes</th>
         <th>Intervalo de IOPS em múltiplos de 100</th>
         </thead>
         <tbody>
         <tr>
         <td>20 - 39 Gi</td>
         <td>100 - 1000 IOPS</td>
         </tr>
         <tr>
         <td>40 - 79 Gi</td>
         <td>100 - 2.000 IOPS</td>
         </tr>
         <tr>
         <td>80 - 99 Gi</td>
         <td>100 - 4.000 IOPS</td>
         </tr>
         <tr>
         <td>100 - 499 Gi</td>
         <td>100 - 6.000 IOPS</td>
         </tr>
         <tr>
         <td>500 - 999 Gi</td>
         <td>100 - 10.000 IOPS</td>
         </tr>
         <tr>
         <td>1000 - 1.999 Gi</td>
         <td>100 - 20.000 IOPS</td>
         </tr>
         <tr>
         <td>2.000 - 2.999 Gi</td>
         <td>200 - 40.000 IOPS</td>
         </tr>
         <tr>
         <td>3.000 - 3.999 Gi</td>
         <td>200 - 48.000 IOPS</td>
         </tr>
         <tr>
         <td>4.000 - 7.999 Gi</td>
         <td>300 - 48.000 IOPS</td>
         </tr>
         <tr>
         <td>8.000 - 9.999 Gi</td>
         <td>500 - 48.000 IOPS</td>
         </tr>
         <tr>
         <td>10.000 - 12.000 Gi</td>
         <td>1000 - 48.000 IOPS</td>
         </tr>
         </tbody></table>

5. Escolha se você deseja manter os seus dados após o cluster ou a solicitação de volume persistente (PVC) ser excluída.
   - Se você desejar manter seus dados, escolha uma classe de armazenamento `retain`. Quando você exclui o PVC, somente ele é excluído. O PV, o dispositivo de armazenamento físico em sua conta de infraestrutura do IBM Cloud e seus dados ainda existem. Para recuperar o armazenamento e usá-lo em seu cluster novamente, deve-se remover o PV e seguir as etapas para [usar armazenamento de bloco existente](#existing_block).
   - Se desejar que o PV, os dados e seu dispositivo de armazenamento de bloco físico sejam excluídos quando você excluir o PVC, escolha uma classe de armazenamento sem `retain`.

6. Escolha se você deseja ser faturado por hora ou mensalmente. Verifique a [precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/block-storage/pricing) para obter mais informações. Por padrão, todos os dispositivos de armazenamento de bloco são provisionados com um tipo de faturamento por hora.

<br />



## Incluindo armazenamento de bloco em apps
{: #add_block}

Crie um persistent volume claim (PVC) para [provisionar dinamicamente](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) o armazenamento de bloco para seu cluster. O provisionamento dinâmico cria automaticamente o volume persistente correspondente (PV) e pede o dispositivo de armazenamento real em sua conta de infraestrutura do IBM Cloud.
{:shortdesc}

O armazenamento de bloco é fornecido com um modo de acesso `ReadWriteOnce`. Só é possível montá-lo em um pod em um nó do trabalhador no cluster de cada vez.
{: note}

Antes de iniciar:
- Se você tiver um firewall, [permita acesso de saída](/docs/containers?topic=containers-firewall#pvc) para os intervalos de IP da infraestrutura do IBM Cloud das zonas em que seus clusters estão para que seja possível criar PVCs.
- Instale o [plug-in de armazenamento de bloco do {{site.data.keyword.cloud_notm}}](#install_block).
- [Decida sobre uma classe de armazenamento predefinida](#block_predefined_storageclass) ou crie uma [classe de armazenamento customizada](#block_custom_storageclass).

Procurando implementar armazenamento de bloco em um conjunto stateful? Para obter mais informações, consulte [Usando armazenamento de bloco em um conjunto stateful](#block_statefulset).
{: tip}

Para incluir o armazenamento de bloco:

1.  Crie um arquivo de configuração para definir a sua solicitação de volume persistente (PVC) e salve a configuração como um arquivo `.yaml`.

    -  **Exemplo para classes de armazenamento bronze, prata, ouro**:
       O arquivo `.yaml` a seguir cria uma solicitação que é denominada `mypvc` da classe de armazenamento `"ibmc-block-silver"`, faturada `"hourly"`, com um tamanho de gigabyte de `24Gi`.

       ```
       apiVersion: v1 kind: PersistentVolumeClaim metadata: name: mypvc labels: billingType: "hourly" 	 region: us-south zone: dal13 spec: accessModes:
           - ReadWriteOnce
         resources:
           requests:
             storage: 24Gi
	     storageClassName: ibmc-block-silver
       ```
       {: codeblock}

    -  **Exemplo para usar a classe de armazenamento customizada**:
       O arquivo `.yaml` a seguir cria uma solicitação que é denominada `mypvc` da classe de armazenamento `ibmc-block-retain-custom`, faturada `"hourly"`, com um tamanho de gigabyte de `45Gi` e IOPS de `"300"`.

       ```
       apiVersion: v1 kind: PersistentVolumeClaim metadata: name: mypvc labels: billingType: "hourly" 	 region: us-south zone: dal13 spec: accessModes:
           - ReadWriteOnce
         resources:
           requests:
             storage: 45Gi
             iops: "300"
	     storageClassName: ibmc-block-retain-custom
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
         <td><code> metadata.labels.billingType </code></td>
         <td>Especifique a frequência para a qual sua conta de armazenamento é calculada, como "mensal" ou "por hora". O padrão é "horária".</td>
       </tr>
       <tr>
       <td><code> metadata.labels.region </code></td>
       <td>Especifique a região na qual você deseja provisionar seu armazenamento de bloco. Se você especifica a região, deve-se também especificar uma zona. Se você não especifica uma região ou a região especificada não é localizada, o armazenamento é criado na mesma região que o seu cluster. <p class="note">Essa opção é suportada somente com o plug-in do IBM Cloud Block Storage versão 1.0.1 ou superior. Para versões de plug-in mais antigas, se você tiver um cluster de múltiplas zonas, a zona na qual o seu armazenamento for provisionado será selecionada em uma base round-robin para balancear as solicitações de volume uniformemente em todas as zonas. Para especificar a zona para seu armazenamento, é possível criar uma [classe de armazenamento customizada](#block_multizone_yaml) primeiro. Em seguida, crie um PVC com a sua classe de armazenamento customizada.</p></td>
       </tr>
       <tr>
       <td><code> metadata.labels.zone </code></td>
	<td>Especifique a zona na qual você deseja provisionar seu armazenamento de bloco. Se você especifica a zona, deve-se também especificar uma região. Se você não especifica uma zona ou a zona especificada não é localizada em um cluster de múltiplas zonas, a zona é selecionada em uma base round-robin. <p class="note">Essa opção é suportada somente com o plug-in do IBM Cloud Block Storage versão 1.0.1 ou superior. Para versões de plug-in mais antigas, se você tiver um cluster de múltiplas zonas, a zona na qual o seu armazenamento for provisionado será selecionada em uma base round-robin para balancear as solicitações de volume uniformemente em todas as zonas. Para especificar a zona para seu armazenamento, é possível criar uma [classe de armazenamento customizada](#block_multizone_yaml) primeiro. Em seguida, crie um PVC com a sua classe de armazenamento customizada.</p></td>
	</tr>
        <tr>
        <td><code> spec.resources.requests.storage </code></td>
        <td>Insira o tamanho do armazenamento de bloco, em gigabytes (Gi). Depois que seu armazenamento for provisionado, não será possível mudar o tamanho de seu armazenamento de bloco. Certifique-se de especificar um tamanho que corresponda à quantia de dados que você deseja armazenar. </td>
        </tr>
        <tr>
        <td><code> spec.resources.requests.iops </code></td>
        <td>Essa opção está disponível somente para as classes de armazenamento customizadas (`ibmc-block-custom/ibmc-block-retain-custom`). Especifique o IOPS total para o armazenamento, selecionando um múltiplo de 100 dentro do intervalo permitido. Se você escolher um IOPS diferente de um que esteja listado, o IOPS será arredondado para cima.</td>
        </tr>
	<tr>
	<td><code> spec.storageClassName </code></td>
	<td>O nome da classe de armazenamento que você deseja usar para provisionar armazenamento de bloco. É possível optar por usar uma das [classes de armazenamento fornecidas pela IBM](#block_storageclass_reference) ou [criar a sua própria](#block_custom_storageclass). </br> Se você não especificar uma classe de armazenamento, o PV será criado com a classe de armazenamento padrão <code>ibmc-file-bronze</code><p>**Dica:** se você desejar mudar a classe de armazenamento padrão, execute <code>oc patch storageclass &lt;storageclass&gt; -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'</code> e substitua <code>&lt;storageclass&gt;</code> pelo nome da classe de armazenamento.</p></td>
	</tr>
        </tbody></table>

    Se você desejar usar uma classe de armazenamento customizada, crie seu PVC com o nome da classe de armazenamento correspondente, um IOPS válido e o tamanho.   
    {: tip}

2.  Crie o PVC.

    ```
    oc apply -f mypvc.yaml
    ```
    {: pre}

3.  Verifique se o PVC foi criado e ligado ao PV. Esse processo pode levar alguns minutos.

    ```
    oc describe pvc mypvc
    ```
    {: pre}

    Saída de exemplo:

    ```
    Name:		mypvc
    Namespace:	default
    StorageClass:	""
    Status:		Bound
    Volume:		pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
    Labels:		<none>
    Capacity:	20Gi
    Access Modes:	RWO
    Events:
      FirstSeen	LastSeen	Count	From								SubObjectPath	Type		Reason			Message
      ---------	--------	-----	----								-------------	--------	------			-------
      3m		3m		1	{ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 }			Normal		Provisioning		External provisioner is provisioning volume for claim "default/my-persistent-volume-claim"
      3m		1m		10	{persistentvolume-controller }							Normal		ExternalProvisioning	cannot find provisioner "ibm.io/ibmc-block", expecting that a volume for the claim is provisioned either manually or via external software
      1m		1m		1	{ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 }			Normal		ProvisioningSucceeded	Successfully provisioned volume pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2

    ```
    {: screen}

4.  {: #block_app_volume_mount}Para montar o PV em sua implementação, crie um arquivo de configuração `.yaml` e especifique o PVC que liga o PV.

    ```
    apiVersion: apps/v1 kind: Deployment metadata: name: <deployment_name> labels: app: <deployment_label> spec: selector: matchLabels: app: <app_name> template: metadata: labels: app: <app_name> spec: containers:
          - image: <image_name>
            name: <container_name>
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
    <td><code> spec.containers.volumeMounts.mountPath </code></td>
    <td>O caminho absoluto do diretório no qual o volume está montado dentro do contêiner. Os dados gravados no caminho de montagem são armazenados sob o diretório-raiz em sua instância de armazenamento de bloco físico. Se você desejar compartilhar um volume entre apps diferentes, será possível especificar [subcaminhos do volume ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath) para cada um de seus apps. </td>
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

<br />




## Usando o armazenamento de bloco existente em seu cluster
{: #existing_block}

Se você tiver um dispositivo de armazenamento físico existente que desejar usar em seu cluster, será possível criar manualmente o PV e o PVC para [provisionar estaticamente](/docs/containers?topic=containers-kube_concepts#static_provisioning) o armazenamento.
{: shortdesc}

Para que seja possível iniciar a montagem de seu armazenamento existente em um app, deve-se recuperar todas as informações necessárias para o seu PV.  

### Etapa 1: recuperando as informações de seu armazenamento de bloco existente
{: #existing-block-1}

1.  Recupere ou gere uma chave de API para sua conta de infraestrutura do IBM Cloud.
    1. Efetue login no [Portal de infraestrutura do IBM Cloud ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/classic?).
    2. Selecione **Conta**, depois **Usuários** e, em seguida, **Lista de usuários**.
    3. Localize seu ID de usuário.
    4. Na coluna **CHAVE API**, clique em **Gerar** para gerar uma chave API ou em **Visualizar** para visualizar a chave API existente.
2.  Recupere o nome do usuário da API para sua conta de infraestrutura do IBM Cloud.
    1. No menu **Lista de usuários**, selecione seu ID de usuário.
    2. Na seção **Informações de acesso da API**, localize o seu **Nome do usuário da API**.
3.  Efetue login no plug-in da CLI da infraestrutura do IBM Cloud.
    ```
    ibmcloud sl init
    ```
    {: pre}

4.  Escolha autenticar usando o nome do usuário e a chave de API para a sua conta de infraestrutura do IBM Cloud.
5.  Insira o nome de usuário e a chave API recuperados nas etapas anteriores.
6.  Liste os dispositivos de armazenamento de bloco disponíveis.
    ```
    ibmcloud sl block volume-list
    ```
    {: pre}

    Saída de exemplo:
    ```
    id         username            datacenter   storage_type              capacity_gb   bytes_used   ip_addr         lunId   active_transactions
    38642141   IBM02SEL1543159-1   dal10        endurance_block_storage   20            -            169.xx.xxx.xxx   170     0
    ```
    {: screen}

7.  Anote o `id`, `ip_addr`, `capacity_gb`, `datacenter` e `lunId` do dispositivo de armazenamento de bloco que você deseja montar em seu cluster. **Nota:** para montar o armazenamento existente em um cluster, deve-se ter um nó do trabalhador na mesma zona que seu armazenamento. Para verificar a zona do seu nó do trabalhador, execute `ibmcloud oc workers --cluster <cluster_name_or_ID>`.

### Etapa 2: Criando um volume persistente (PV) e uma solicitação de volume persistente correspondente (PVC)
{: #existing-block-2}

1.  Opcional: se você tiver o armazenamento provisionado com uma classe de armazenamento `retain`, quando remover o PVC, o PV e o dispositivo de armazenamento físico não serão removidos. Para reutilizar o armazenamento em seu cluster, deve-se remover o PV primeiro.
    1. Liste PVs existentes.
       ```
       oc get pv
       ```
       {: pre}

       Procure o PV que pertence ao seu armazenamento persistente. O PV está em um estado `released`.

    2. Remova o PV.
       ```
       oc delete pv <pv_name>
       ```
       {: pre}

    3. Verifique se o PV foi removido.
       ```
       oc get pv
       ```
       {: pre}

2.  Crie um arquivo de configuração para seu PV. Inclua o armazenamento de bloco `id`, `ip_addr`, `capacity_gb`, `datacenter` e `lunIdID` que você recuperou anteriormente.

    ```
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: mypv
      labels:
         failure-domain.beta.kubernetes.io/region: <region>
         failure-domain.beta.kubernetes.io/zone: <zone>
    spec:
      capacity:
        storage: "<storage_size>"
      accessModes:
        - ReadWriteOnce
      flexVolume:
        driver: "ibm/ibmc-block"
        fsType: "<fs_type>"
        options:
          "Lun": "<lun_ID>"
          "TargetPortal": "<IP_address>"
          "VolumeID": "<volume_ID>"
          "volumeName": "<volume_name>"
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
    <td>Insira o nome do PV que você deseja criar.</td>
    </tr>
    <tr>
    <td><code>metadata.labels</code></td>
    <td>Insira a região e a zona que você recuperou anteriormente. Deve-se ter pelo menos um nó do trabalhador na mesma região e zona que o seu armazenamento persistente para montar o armazenamento em seu cluster. Se um PV para o seu armazenamento já existir, [inclua o rótulo de zona e região](/docs/containers?topic=containers-kube_concepts#storage_multizone) em seu PV.
    </tr>
    <tr>
    <td><code> spec.flexVolume.fsType </code></td>
    <td>Insira o tipo de sistema de arquivos que está configurado para seu armazenamento de bloco existente. Escolha entre <code>ext4</code> ou <code>xfs</code>. Se você não especificar essa opção, o PV assumirá o padrão para <code>ext4</code>. Quando o `fsType` errado for definido, a criação do PV será bem-sucedida, mas a montagem do PV em um pod falhará. </td></tr>	    
    <tr>
    <td><code> spec.capacity.storage </code></td>
    <td>Insira o tamanho da área de armazenamento do armazenamento de bloco existente recuperado na etapa anterior como <code>capacity-gb</code>. O tamanho do armazenamento deve ser gravado em gigabytes, por exemplo, 20 Gi (20 GB) ou 1000 Gi (1 TB).</td>
    </tr>
    <tr>
    <td><code> flexVolume.options.Lun </code></td>
    <td>Insira o ID de LUN para o armazenamento de bloco que você recuperou anteriormente como <code>lunId</code>.</td>
    </tr>
    <tr>
    <td><code> flexVolume.options.TargetPortal </code></td>
    <td>Insira o endereço IP do armazenamento de bloco que você recuperou anteriormente como <code>ip_addr</code>. </td>
    </tr>
    <tr>
	    <td><code> flexVolume.options.VolumeId </code></td>
	    <td>Insira o ID do armazenamento de bloco que você recuperou anteriormente como <code>id</code>.</td>
	    </tr>
	    <tr>
		    <td><code> flexVolume.options.volumeName </code></td>
		    <td>Insira um nome para seu volume.</td>
	    </tr>
    </tbody></table>

3.  Crie o PV em seu cluster.
    ```
    oc apply -f mypv.yaml
    ```
    {: pre}

4. Verifique se o PV é criado.
    ```
    oc get pv
    ```
    {: pre}

5. Crie outro arquivo de configuração para criar seu PVC. Para que o PVC corresponda ao PV criado anteriormente, deve-se escolher o mesmo valor para `storage` e `accessMode`. O campo `storage-class` deve estar vazio. Se algum desses campos não corresponder ao PV, um novo PV será criado automaticamente no lugar.

     ```
     kind: PersistentVolumeClaim apiVersion: v1 metadata: name: mypvc spec: accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: "<storage_size>"
      storageClassName:
     ```
     {: codeblock}

6.  Crie seu PVC.
     ```
     oc apply -f mypvc.yaml
     ```
     {: pre}

7.  Verifique se o PVC foi criado e está ligado ao PV criado anteriormente. Esse processo pode levar alguns minutos.
     ```
     oc describe pvc mypvc
     ```
     {: pre}

     Saída de exemplo:

     ```
     Name: mypvc
    Namespace: default
    StorageClass: ""
     Status: Bound
     Volume: pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
     Labels: <none>
     Capacity: 20Gi
     Access Modes: RWO
     Events:
       FirstSeen LastSeen Count From        SubObjectPath Type Reason Message
       --------- -------- ----- ----        ------------- -------- ------ -------
       3m 3m 1 {ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 } Normal Provisioning External provisioner is provisioning volume  for claim "default/my-persistent-volume-claim"
       3m 1m	 10 {persistentvolume-controller } Normal ExternalProvisioning cannot find provisioner "ibm.io/ibmc-block", expecting that  a volume for the claim is provisioned either manually or via external software
       1m 1m 1 {ibm.io/ibmc-block 31898035-3011-11e7-a6a4-7a08779efd33 } Normal ProvisioningSucceeded	Successfully provisioned volume  pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
     ```
     {: screen}

Você criou com êxito um PV e ligou-o a um PVC. Os usuários do cluster agora podem [montar o PVC](#block_app_volume_mount) em suas implementações e começar a ler e gravar no PV.

<br />



## Usando o armazenamento de bloco em um conjunto stateful
{: #block_statefulset}

Se você tiver um app stateful como um banco de dados, será possível criar conjuntos stateful que usam armazenamento de bloco para armazenar os dados de seu app. Como alternativa, é possível usar um banco de dados como um serviço do {{site.data.keyword.cloud_notm}} e armazenar seus dados na nuvem.
{: shortdesc}

**De que eu preciso estar ciente ao incluir armazenamento de bloco em um conjunto stateful?** </br>
Para incluir armazenamento em um conjunto stateful, especifique sua configuração de armazenamento na seção `volumeClaimTemplates` do YAML do conjunto stateful. O `volumeClaimTemplates` é a base para seu PVC e pode incluir a classe de armazenamento e o tamanho ou IOPS do armazenamento de bloco que você deseja provisionar. No entanto, se você desejar incluir rótulos nos `volumeClaimTemplates`, os Kubernetes não incluirão esses rótulos ao criar o PVC. Em vez disso, deve-se incluir os rótulos diretamente no conjunto stateful.

Não é possível implementar dois conjuntos stateful ao mesmo tempo. Se você tentar criar um conjunto stateful antes que um diferente seja totalmente implementado, a implementação do conjunto stateful poderá levar a resultados inesperados.
{: important}

**Como posso criar meu conjunto stateful em uma zona específica?** </br>
Em um cluster com várias zonas, é possível especificar a zona e a região em que você deseja criar seu conjunto stateful nas seções `spec.selector.matchLabels` e `spec.template.metadata.labels` do YAML do conjunto stateful. Como alternativa, é possível incluir esses rótulos em uma [classe de armazenamento customizada](/docs/containers?topic=containers-kube_concepts#customized_storageclass) e usar essa classe de armazenamento na seção `volumeClaimTemplates` de seu conjunto stateful.

**Posso atrasar a ligação de um PV ao meu pod stateful até que o pod esteja pronto?**<br>
Sim, é possível [criar uma classe de armazenamento customizada](#topology_yaml) para seu PVC que inclui o campo [`volumeBindingMode: WaitForFirstConsumer` ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode).

**Quais opções eu tenho para incluir armazenamento de bloco em um conjunto stateful?** </br>
Se você desejar criar automaticamente seu PVC ao criar o conjunto stateful, use o [fornecimento dinâmico](#block_dynamic_statefulset). Também é possível optar por [pré-provisionar os PVCs ou usar PVCs existentes](#block_static_statefulset) com o conjunto stateful.  

### Fornecimento dinâmico: criando o PVC ao criar um conjunto stateful
{: #block_dynamic_statefulset}

Use essa opção se desejar criar automaticamente o PVC ao criar o conjunto stateful.
{: shortdesc}

Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Verifique se todos os conjuntos stateful existentes no cluster estão totalmente implementados. Se um conjunto stateful ainda estiver sendo implementado, não será possível iniciar a criação do conjunto stateful. Deve-se aguardar até que todos os conjuntos stateful no cluster estejam totalmente implementados para evitar resultados inesperados.
   1. Liste os conjuntos stateful existentes em seu cluster.
      ```
      oc get statefulset --all-namespaces
      ```
      {: pre}

      Saída de exemplo:
      ```
      NAME DESIRED CURRENT AGE mystatefulset 3 3 6s
      ```
      {: screen}

   2. Visualize o **Status dos pods** de cada conjunto stateful para assegurar-se de que a implementação do conjunto stateful esteja concluída.  
      ```
      oc describe statefulset <statefulset_name>
      ```
      {: pre}

      Saída de exemplo:
      ```
      Nome:               nginx
      Namespace:          default
      CreationTimestamp:  Fri, 05 Oct 2018 13:22:41 -0400
      Seletor:            app=nginx,billingType=hourly,region=us-south,zone=dal10
      Rótulos:            app=nginx
                          billingType=hourly
                          region=us-south
                          zone=dal10
      Anotações:        oc.kubernetes.io/last-applied-configuration={"apiVersion":"apps/v1","kind":"StatefulSet","metadata":{"annotations":{},"name":"nginx","namespace":"default"},"spec":{"podManagementPolicy":"Par...
      Réplicas:           3 desejados | 3 total
      Status de pods:        0 Em execução / 3 Aguardando / 0 Bem-sucedidos / 0 Com falha
      Modelo de pod:
        Rótulos:  app=nginx
                 billingType=hourly
                 region=us-south
                 zone=dal10
      ...
      ```
      {: screen}

      Um conjunto stateful é totalmente implementado quando o número de réplicas localizadas na seção **Réplicas** de sua saída da CLI é igual ao número de pods **Em execução** na seção **Status dos pods**. Se um conjunto stateful ainda não estiver totalmente implementado, aguarde até que a implementação seja concluída antes de continuar.

2. Crie um arquivo de configuração para seu conjunto stateful e o serviço usado para expor o conjunto stateful.

   - **Exemplo de conjunto stateful que especifica uma zona:**

     O exemplo a seguir mostra como implementar NGINX como um conjunto stateful com três réplicas. Para cada réplica, um dispositivo de armazenamento de bloco de 20 gigabyte é provisionado com base nas especificações que são definidas na classe de armazenamento `ibmc-block-retain-bronze`. Todos os dispositivos de armazenamento são provisionados na zona `dal10`. Como o armazenamento de bloco não pode ser acessado por meio de outras zonas, todas as réplicas do conjunto stateful também são implementadas nos nós do trabalhador que estão localizados em `dal10`.

     ```
     apiVersion: v1 kind: Service metadata: name: nginx labels: app: nginx spec: ports:
      - port: 80 name: web clusterIP: None selector: app: nginx
     ---
     apiVersion: apps/v1 kind: StatefulSet metadata: name: nginx spec: serviceName: "nginx" replicas: 3 podManagementPolicy: Parallel selector: matchLabels: app: nginx billingType: "hourly" region: "us-south" zone: "dal10" template: metadata: labels: app: nginx billingType: "hourly" region: "us-south" zone: "dal10" spec: containers:
          - name: nginx image: k8s.gcr.io/nginx-slim:0.8 ports:
            - containerPort: 80 name: web volumeMounts:
            - name: myvol mountPath: /usr/share/nginx/html volumeClaimTemplates:
      - metadata: name: myvol spec: accessModes:
          - ReadWriteOnce
          resources:
            requests:
              storage: 20Gi
              iops: "300" #required only for performance storage
	      storageClassName: ibmc-block-retain-bronze
     ```
     {: codeblock}

   - **Exemplo de conjunto stateful com antiafinidade de regra e criação de armazenamento de bloco atrasado:**

     O exemplo a seguir mostra como implementar NGINX como um conjunto stateful com três réplicas. O conjunto stateful não especifica a região e a zona em que o armazenamento de bloco é criado. Em vez disso, o conjunto stateful usa uma regra de antiafinidade para assegurar que os pods sejam difundidos entre os nós do trabalhador e as zonas. Definindo `topologykey: failure-domain.beta.kubernetes.io/zone`, o planejador do Kubernetes não poderá planejar um pod em um nó do trabalhador se o nó do trabalhador estiver na mesma zona que um pod que tenha o rótulo `app: nginx`. Para cada pod do conjunto stateful, dois PVCs são criados conforme definido na seção `volumeClaimTemplates`, mas a criação das instâncias de armazenamento de bloco é atrasada até que um pod do conjunto stateful que use o armazenamento seja planejado. Essa configuração é referida como [planejamento de volume com reconhecimento de topologia](https://kubernetes.io/blog/2018/10/11/topology-aware-volume-provisioning-in-kubernetes/).

     ```
     apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: ibmc-block-bronze-delayed parameters: billingType: hourly classVersion: "2" fsType: ext4 iopsPerGB: "2" sizeRange: '[20-12000]Gi' type: Endurance provisioner: ibm.io/ibmc-block reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer
     ---
     apiVersion: v1 kind: Service metadata: name: nginx labels: app: nginx spec: ports:
       - port: 80 name: web clusterIP: None selector: app: nginx
     ---
     apiVersion: apps/v1 kind: StatefulSet metadata: name: web spec: serviceName: "nginx" replicas: 3 podManagementPolicy: "Parallel" selector: matchLabels: app: nginx template: metadata: labels: app: nginx spec: affinity: podAntiAffinity: preferredDuringSchedulingIgnoredDuringExecution:
               - weight: 100
            podAffinityTerm:
              labelSelector:
                matchExpressions:
                     - key: app
                  operator: In
                  values:
                       - nginx topologyKey: failure-domain.beta.kubernetes.io/zone containers:
           - name: nginx image: k8s.gcr.io/nginx-slim:0.8 ports:
             - containerPort: 80 name: web volumeMounts:
             - name: myvol1
               mountPath: /usr/share/nginx/html
             - name: myvol2
               mountPath: /tmp1
       volumeClaimTemplates:
       - metadata: name: myvol1 spec: accessModes:
           - ReadWriteOnce # access mode resources: requests: storage: 20Gi 	 storageClassName: ibmc-block-bronze-delayed
       - metadata: name: myvol2 spec: accessModes:
           - ReadWriteOnce # access mode resources: requests: storage: 20Gi 	 storageClassName: ibmc-block-bronze-delayed
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
     <td style="text-align:left"><code> spec.podManagementPolicy </code></td>
     <td style="text-align:left">Insira a política de gerenciamento de pod que deseja usar para o conjunto stateful. Escolha entre as opções a seguir: <ul><li><strong>`OrderedReady`: </strong>Com essa opção, as réplicas do conjunto stateful são implementadas uma após a outra. Por exemplo, se você especificou três réplicas, o Kubernetes criará o PVC para a sua primeira réplica, esperará até que o PVC seja ligado, implementará a réplica do conjunto stateful e montará o PVC na réplica. Depois que a implementação é concluída, a segunda réplica é implementada. Para obter mais informações sobre essa opção, consulte [Gerenciamento de pod `OrderedReady` ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#orderedready-pod-management). </li><li><strong>Paralelo: </strong> com essa opção, a implementação de todas as réplicas do conjunto stateful é iniciada ao mesmo tempo. Se o seu app suportar a implementação paralela de réplicas, use essa opção para economizar tempo de implementação para seus PVCs e réplicas do conjunto stateful. </li></ul></td>
     </tr>
     <tr>
     <td style="text-align:left"><code> spec.selector.matchLabels </code></td>
     <td style="text-align:left">Insira todos os rótulos que deseja incluir no conjunto stateful e no PVC. Os rótulos incluídos no <code>volumeClaimTemplates</code> de seu conjunto stateful não são reconhecidos pelo Kubernetes. Os rótulos de amostra que você pode desejar incluir são: <ul><li><code><strong>region</strong></code> e <code><strong>zone</strong></code>: se você desejar que todas as réplicas e PVCs do conjunto stateful sejam criados em uma zona específica, inclua ambos os rótulos. Também é possível especificar a zona e a região na classe de armazenamento usada. Se você não especificar uma zona e uma região e tiver um cluster com várias zonas, a zona na qual seu armazenamento é provisionado será selecionada em uma base round-robin para balancear solicitações de volume uniformemente em todas as zonas.</li><li><code><strong>billingType</strong></code>: insira o tipo de faturamento que você deseja usar para seus PVCs. Escolha entre  <code> horária </code>  ou  <code> mensal </code>. Se você não especificar esse rótulo, todos os PVCs serão criados com um tipo de faturamento por hora. </li></ul></td>
     </tr>
     <tr>
     <td style="text-align:left"><code> spec.template.metadata.labels </code></td>
     <td style="text-align:left">Insira os mesmos rótulos incluídos na seção <code>spec.selector.matchLabels</code>. </td>
     </tr>
     <tr>
     <td style="text-align:left"><code> spec.template.spec.affinity </code></td>
     <td style="text-align:left">Especifique sua regra de antiafinidade para assegurar que seus pods do conjunto stateful sejam distribuídos entre os nós do trabalhador e as zonas. O exemplo mostra uma regra de antiafinidade em que o pod do conjunto stateful prefere não ser planejado em um nó do trabalhador no qual um pod que tem o rótulo `app: nginx` é executado. O `topologykey: failure-domain.beta.kubernetes.io/zone` restringe essa regra de antiafinidade ainda mais e evita que o pod seja planejado em um nó trabalhador se o nó do trabalhador estiver na mesma zona que um pod que possui o rótulo `app: nginx`. Usando essa regra de antiafinidade, é possível alcançar a antiafinidade entre os nós do trabalhador e as zonas. </td>
     </tr>
     <tr>
     <td style="text-align:left"><code> spec.volumeClaimTemplates.metadata.name </code></td>
     <td style="text-align:left">Insira um nome para seu volume. Use o mesmo nome definido na seção <code>spec.containers.volumeMount.name</code>. O nome inserido aqui é usado para criar o nome para seu PVC no formato: <code>&lt;volume_name&gt;-&lt;statefulset_name&gt;-&lt;replica_number&gt;</code>. </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.resources.</code></br><code>requests.storage</code></td>
     <td style="text-align:left">Insira o tamanho do armazenamento de bloco em gigabytes (Gi).</td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.resources.</code></br><code>requests.iops</code></td>
     <td style="text-align:left">Se você desejar fornecer o [armazenamento de desempenho](#block_predefined_storageclass), insira o número de IOPS. Se você usar uma classe de armazenamento do Endurance e especificar vários IOPS, o número de IOPS será ignorado. Em vez disso, o IOPS especificado em sua classe de armazenamento é usado.  </td>
     </tr>
     <tr>
     <td style="text-align:left"><code>spec.volumeClaimTemplates.</code></br><code>spec.storageClassName</code></td>
     <td style="text-align:left">Insira a classe de armazenamento que deseja usar. Para listar as classes de armazenamento existentes, execute <code>oc get storageclasses | grep block</code>. Se você não especificar uma classe de armazenamento, o PVC será criado com a classe de armazenamento padrão configurada em seu cluster. Certifique-se de que a classe de armazenamento padrão use o provisionador <code>ibm.io/ibmc-block</code> para que seu conjunto stateful seja provisionado com armazenamento de bloco.</td>
     </tr>
     </tbody></table>

4. Crie seu conjunto stateful.
   ```
   oc apply -f statefulset.yaml
   ```
   {: pre}

5. Aguarde o seu conjunto stateful ser implementado.
   ```
   oc describe statefulset <statefulset_name>
   ```
   {: pre}

   Para ver o status atual de suas PVCs, execute `oc get pvc`. O nome de sua PVC é formatado como `<volume_name>-<statefulset_name>-<replica_number>`.
   {: tip}

### Fornecimento estático: usando PVCs existentes com um conjunto stateful
{: #block_static_statefulset}

É possível pré-provisionar seus PVCs antes de criar seu conjunto stateful ou usar PVCs existentes com esse conjunto.
{: shortdesc}

Quando você [provisionar dinamicamente seus PVCs ao criar o conjunto stateful](#block_dynamic_statefulset), o nome do PVC será designado com base nos valores usados no arquivo YAML do conjunto stateful. Para que o conjunto stateful use PVCs existentes, o nome dos PVCs deve corresponder ao nome que seria criado automaticamente ao usar o fornecimento dinâmico.

Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Se você desejar pré-fornecer o PVC para seu conjunto stateful antes de criar o conjunto stateful, siga as etapas de 1 a 3 em [Incluindo armazenamento de bloco em apps](#add_block) para criar um PVC para cada réplica do conjunto stateful. Certifique-se de criar sua PVC com um nome que siga o formato a seguir: `<volume_name>-<statefulset_name>-<replica_number>`.
   - **`<volume_name>`**: use o nome que você deseja especificar na seção `spec.volumeClaimTemplates.metadata.name` de seu conjunto stateful, como `nginxvol`.
   - **`<statefulset_name>`**: use o nome que você deseja especificar na seção `metadata.name` de seu conjunto stateful, como `nginx_statefulset`.
   - **`<replica_number>`**: Insira o número de sua réplica, iniciando com 0.

   Por exemplo, se três réplicas de conjunto stateful devem ser criadas, crie três PVCs com nomes a seguir: `nginxvol-nginx_statefulset-0`, `nginxvol-nginx_statefulset-1` e `nginxvol-nginx_statefulset-2`.  

   Procurando criar um PVC e um PV para um dispositivo de armazenamento existente? Crie seu PVC e PV usando o [fornecimento estático](#existing_block).

2. Siga as etapas em [Fornecimento dinâmico: criando o PVC ao criar um conjunto stateful](#block_dynamic_statefulset) para criar seu conjunto stateful. O nome de sua PVC segue o formato `<volume_name>-<statefulset_name>-<replica_number>`. Certifique-se de usar os valores a seguir de seu nome do PVC na especificação do conjunto stateful:
   - **`spec.volumeClaimTemplates.metadata.name`**: insira o `<volume_name>` do nome de sua PVC.
   - **`metadata.name`**: insira o `<statefulset_name>` do nome de sua PVC.
   - **`spec.replicas`**: insira o número de réplicas que você deseja criar para seu conjunto stateful. O número de réplicas deve ser igual ao número de PVCs criados anteriormente.

   Se seus PVCs estiverem em zonas diferentes, não inclua um rótulo de região ou zona em seu conjunto stateful.
   {: note}

3. Verifique se os PVCs são usados nos pods de réplica do conjunto stateful.
   1. Liste os pods em seu cluster. Identifique os pods que pertencem ao conjunto stateful.
      ```
      oc get pods
      ```
      {: pre}

   2. Verifique se o PVC existente está montado na réplica do conjunto stateful. Revise o **`ClaimName`** na seção **`Volumes`** de sua saída da CLI.
      ```
      oc describe pod <pod_name>
      ```
      {: pre}

      Saída de exemplo:
      ```
      Name: nginx-0 Namespace: default Node: 10.xxx.xx.xxx/10.xxx.xx.xxx Start Time: Fri, 05 Oct 2018 13:24:59 -0400 ...
      Volumes: myvol: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: myvol-nginx-0 ...
      ```
      {: screen}

<br />


## Mudando o tamanho e o IOPS de seu dispositivo de armazenamento existente
{: #block_change_storage_configuration}

Se você desejar aumentar a capacidade de armazenamento ou o desempenho, será possível modificar seu volume existente.
{: shortdesc}

Para perguntas sobre faturamento e para localizar as etapas de como usar o console do {{site.data.keyword.cloud_notm}} para modificar seu armazenamento, consulte [Expandindo a capacidade do Block Storage](/docs/infrastructure/BlockStorage?topic=BlockStorage-expandingcapacity#expandingcapacity) e [Ajustando o IOPS](/docs/infrastructure/BlockStorage?topic=BlockStorage-adjustingIOPS). As atualizações que você faz por meio do console não são refletidas no volume persistente (PV). Para incluir essas informações no PV, execute `oc patch pv <pv_name>` e atualize manualmente o tamanho e o IOPS nas seções **Rótulos** e **Anotação** do seu PV.
{: tip}

1. Liste os PVCs em seu cluster e anote o nome do PV associado na coluna **VOLUME**.
   ```
   oc get pvc
   ```
   {: pre}

   Saída de exemplo:
   ```
   NAME             STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS        AGE
   myvol            Bound     pvc-01ac123a-123b-12c3-abcd-0a1234cb12d3   20Gi       RWO            ibmc-block-bronze    147d
   ```
   {: screen}

2. Se você desejar mudar o IOPS e o tamanho para seu armazenamento de bloco, edite o IOPS na seção `metadata.labels.IOPS` de seu PV primeiro. É possível mudar para um valor de IOPS inferior ou superior. Certifique-se de inserir um IOPS que seja suportado para o tipo de armazenamento que você tem. Por exemplo, se você tiver armazenamento de bloco do Endurance com 4 IOPS, será possível mudar o IOPS para 2 ou 10. Para obter mais valores de IOPS suportados, consulte [Decidindo sobre a configuração de armazenamento de bloco](/docs/containers?topic=containers-block_storage#block_predefined_storageclass).
   ```
   oc edit pv <pv_name>
   ```
   {: pre}

   Para mudar o IOPS por meio da CLI, deve-se também mudar o tamanho do seu armazenamento de bloco. Se você deseja mudar somente o IOPS, mas não o tamanho, deve-se [solicitar a mudança de IOPS por meio do console](/docs/infrastructure/BlockStorage?topic=BlockStorage-adjustingIOPS).
   {: note}

3. Edite a PVC e inclua o novo tamanho na seção `spec.resources.requests.storage` de sua PVC. É possível mudar para um tamanho maior somente até a capacidade máxima que é configurada por sua classe de armazenamento. Não é possível reduzir seu armazenamento existente. Para ver os tamanhos disponíveis para sua classe de armazenamento, consulte [Decidindo sobre a configuração de armazenamento de bloco](/docs/containers?topic=containers-block_storage#block_predefined_storageclass).
   ```
   oc edit pvc <pvc_name>
   ```
   {: pre}

4. Verifique se a expansão de volume foi solicitada. A expansão de volume foi solicitada com êxito quando você vê uma mensagem `FileSystemResizePending` na seção **Condições** de sua saída da CLI. 
   ```
   oc describe pvc <pvc_name>
   ```
   {: pre}

   Saída de exemplo:
   ```
   ...
   Conditions:
   Type                      Status  LastProbeTime                     LastTransitionTime                Reason  Message
   ----                      ------  -----------------                 ------------------                ------  -------
   FileSystemResizePending   True    Mon, 01 Jan 0001 00:00:00 +0000   Thu, 25 Apr 2019 15:52:49 -0400           Waiting for user to (re-)start a pod to finish file system resize of volume on node.
   ```
   {: screen}

5. Liste todos os pods que montam a PVC. Se a PVC for montada por um pod, a expansão de volume será processada automaticamente. Se a sua PVC não for montada por um pod, a PVC deverá ser montada em um pod para que a expansão de volume possa ser processada. 
   ```
   oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
   ```
   {: pre}

   Os pods montados são retornados no formato: `<pod_name>: <pvc_name>`.

6. Se a PVC não for montada por um pod, [crie um pod ou uma implementação e monte a PVC](/docs/containers?topic=containers-block_storage#add_block). Se a PVC for montada por um pod, continue com a próxima etapa. 

7. Monitore o status de expansão de volume. A expansão de volume é concluída quando você vê a mensagem `"message":"Success"` em sua saída da CLI.
   ```
   oc get pv <pv_name> -o go-template=$'{{index .metadata.annotations "ibm.io/volume-expansion-status"}}\n'
   ```
   {: pre}

   Saída de exemplo:
   ```
   {"size":50,"iops":500,"orderid":38832711,"start":"2019-04-30T17:00:37Z","end":"2019-04-30T17:05:27Z","status":"complete","message":"Success"}
   ```
   {: screen}

8. Verifique se o tamanho e o IOPS são mudados na seção **Rótulos** de sua saída da CLI.
   ```
   oc describe pv <pv_name>
   ```
   {: pre}

   Saída de exemplo:
   ```
   ...
   Labels:       CapacityGb=50
                 Datacenter=dal10
                 IOPS=500
   ```
   {: screen}


## Fazendo backup e restaurando dados
{: #block_backup_restore}

O armazenamento de bloco é provisionado no mesmo local que os nós do trabalhador em seu cluster. O armazenamento é hospedado em servidores em cluster pela IBM para fornecer disponibilidade no caso de um servidor ficar inativo. No entanto, o armazenamento de bloco não será submetido a backup automaticamente e poderá estar inacessível se o local inteiro falhar. Para proteger seus dados contra perda ou danos, será possível configurar backups periódicos que poderão ser usados para restaurar seus dados quando necessário.
{: shortdesc}

Revise as opções de backup e restauração a seguir para seu armazenamento de bloco:

<dl>
  <dt>Configurar capturas instantâneas periódicas</dt>
  <dd><p>É possível [configurar capturas instantâneas periódicas para o seu armazenamento de bloco](/docs/infrastructure/BlockStorage?topic=BlockStorage-snapshots#snapshots), que é uma imagem somente leitura que captura o estado da instância em um momento. Para armazenar a captura instantânea, deve-se solicitar espaço de captura instantânea em seu armazenamento de bloco. As capturas instantâneas são armazenadas na instância de armazenamento existente dentro da mesma zona. Será possível restaurar dados de uma captura instantânea se um usuário acidentalmente remover dados importantes do volume.</br></br> <strong>Para criar uma captura instantânea para seu volume: </strong><ol><li>[Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)</li><li>Efetue login na CLI `ibmcloud sl`. <pre class="pre"><code>    ibmcloud sl init
    </code></pre></li><li>PVs de Lista existente em seu cluster. <pre class="pre"><code>oc get pv</code></pre></li><li>Obtenha os detalhes para o PV para o qual você deseja criar espaço de captura instantânea e anote o ID do volume, o tamanho e o IOPS. <pre class="pre"><code>oc describe pv &lt;pv_name&gt;</code></pre> O tamanho e o IOPS são mostrados na seção <strong>Labels</strong> de sua saída da CLI. Para localizar o ID do volume, revise a anotação <code>ibm.io/network-storage-id</code> de sua saída da CLI. </li><li>Crie o tamanho da captura instantânea para o volume existente com os parâmetros que você recuperou na etapa anterior. <pre class="pre"><code>ibmcloud sl block snapshot-order &lt;volume_ID&gt; --size &lt;size&gt; --tier &lt;iops&gt;</code></pre></li><li>Espere o tamanho da captura instantânea para criar. <pre class="pre"><code> ibmcloud sl block volume-detail  &lt;volume_ID&gt; </code></pre>O tamanho da captura instantânea é provisionado com êxito quando o <strong>Tamanho da captura instantânea (GB)</strong> na saída da CLI muda de 0 para o tamanho solicitado. </li><li>Crie a captura instantânea para o volume e anote o ID da captura instantânea que é criado para você. <pre class="pre"><code> ibmcloud sl block snapshot-create  &lt;volume_ID&gt; </code></pre></li><li>Verifique se a captura instantânea foi criada com êxito. <pre class="pre"><code> ibmcloud sl block snapshot-list  &lt;volume_ID&gt; </code></pre></li></ol></br><strong>Para restaurar dados por meio de uma captura instantânea para um volume existente: </strong><pre class="pre"><code> ibmcloud sl block snapshot-restore  &lt;volume_ID&gt;  &lt;snapshot_ID&gt; </code></pre></p></dd>
  <dt>Replicar capturas instantâneas para outra zona</dt>
 <dd><p>Para proteger seus dados de uma falha de zona, é possível [replicar capturas instantâneas](/docs/infrastructure/BlockStorage?topic=BlockStorage-replication#replication) para uma instância de armazenamento de bloco que está configurada em outra zona. Os dados podem ser replicados do armazenamento primário para o armazenamento de backup somente. Não é possível montar uma instância de armazenamento de bloco replicada em um cluster. Quando seu armazenamento primário falha, é possível configurar manualmente o armazenamento de backup replicado para ser o primário. Em seguida, é possível montá-lo para seu cluster. Depois que o armazenamento primário é restaurado, é possível restaurar os dados do armazenamento de backup.</p></dd>
 <dt>Armazenamento duplicado</dt>
 <dd><p>É possível [duplicar sua instância de armazenamento de bloco](/docs/infrastructure/BlockStorage?topic=BlockStorage-duplicatevolume#duplicatevolume) na mesma zona que a instância de armazenamento original. Uma duplicata tem os mesmos dados que a instância de armazenamento original no momento em que é criada. Diferentemente de réplicas, use a duplicata como uma instância de armazenamento independente da original. Para duplicar, primeiramente configure capturas instantâneas para o volume.</p></dd>
  <dt>Faça backup dos dados para {{site.data.keyword.cos_full}}</dt>
  <dd><p>É possível usar a [**imagem ibm-backup-restore**](/docs/services/RegistryImages/ibm-backup-restore?topic=RegistryImages-ibmbackup_restore_starter#ibmbackup_restore_starter) para ativar um backup e restaurar o pod em seu cluster. Esse pod contém um script para executar um backup único ou periódico para qualquer persistent volume claim (PVC) em seu cluster. Os dados são armazenados em sua instância do {{site.data.keyword.cos_full}} que você configurou em uma zona.</p><p class="note">O armazenamento de bloco é montado com um modo de acesso RWO. Esse acesso permite que somente um pod seja montado no armazenamento de bloco de cada vez. Para fazer backup de seus dados, deve-se desmontar o pod do aplicativo do armazenamento, montá-lo em seu pod de backup, fazer backup dos dados e remontar o armazenamento para o pod do aplicativo. </p>
Para tornar os seus dados ainda mais altamente disponíveis e proteger o seu app de uma falha de zona, configure uma segunda instância do {{site.data.keyword.cos_short}} e replique dados entre as zonas. Se você precisa restaurar dados de sua instância do {{site.data.keyword.cos_short}}, use o script de restauração que é fornecido com a imagem.</dd>
<dt>Copiar dados de e para pods e contêineres</dt>
<dd><p>É possível usar o [comando![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/reference/kubectl/overview/#cp) `oc cp` para copiar arquivos e diretórios para e por meio de pods ou contêineres específicos em seu cluster.</p>
<p>Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Se você não especificar um contêiner com <code>-c</code>, o comando usará o primeiro contêiner disponível no pod.</p>
<p>É possível usar o comando de várias maneiras:</p>
<ul>
<li>Copie dados de sua máquina local para um pod em seu cluster:<pre class="pre"><code>oc cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var></code></pre></li>
<li>Copie dados de um pod em seu cluster para sua máquina local: <pre class="pre"><code>oc cp <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;/&lt;filename&gt;</var> <var>&lt;local_filepath&gt;/&lt;filename&gt;</var></code></pre></li>
<li>Copiar dados de sua máquina local para um contêiner específico que é executado em um pod em seu cluster: <pre class="pre"><code>oc cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var> -c <var>&lt;container&gt;</var></code></pre></li>
</ul></dd>
  </dl>

<br />


## Referência de classe de armazenamento
{: #block_storageclass_reference}

### Bronze
{: #block_bronze}

<table>
<caption>Classe de armazenamento de bloco: bronze</caption>
<thead>
<th>Características</th>
<th>Configuração</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-block-bronze</code></br><code>ibmc-block-retain-bronze</code></td>
</tr>
<tr>
<td>Tipo</td>
<td>[Armazenamento do Endurance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance)</td>
</tr>
<tr>
<td>Sistema de arquivos</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS por gigabyte</td>
<td>2</td>
</tr>
<tr>
<td>Intervalo de tamanho em gigabytes</td>
<td>20-12.000 Gi</td>
</tr>
<tr>
<td>Disco rígido</td>
<td>SSD</td>
</tr>
<tr>
<td>Faturamento</td>
<td>O tipo de faturamento padrão depende da versão de seu plug-in do {{site.data.keyword.cloud_notm}} Block Storage: <ul><li> Versão 1.0.1 e superior: por hora</li><li>Versão 1.0.0 e inferior: mensal</li></ul></td>
</tr>
<tr>
<td>Precificação</td>
<td>[Informações de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>


### Prata
{: #block_silver}

<table>
<caption>Classe de armazenamento de bloco: prata</caption>
<thead>
<th>Características</th>
<th>Configuração</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-block-silver</code></br><code>ibmc-block-retain-silver</code></td>
</tr>
<tr>
<td>Tipo</td>
<td>[Armazenamento do Endurance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance)</td>
</tr>
<tr>
<td>Sistema de arquivos</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS por gigabyte</td>
<td>4</td>
</tr>
<tr>
<td>Intervalo de tamanho em gigabytes</td>
<td>20-12.000 Gi</td>
</tr>
<tr>
<td>Disco rígido</td>
<td>SSD</td>
</tr>
<tr>
<td>Faturamento</td>
<td>O tipo de faturamento padrão depende da versão de seu plug-in do {{site.data.keyword.cloud_notm}} Block Storage: <ul><li> Versão 1.0.1 e superior: por hora</li><li>Versão 1.0.0 e inferior: mensal</li></ul></td>
</tr>
<tr>
<td>Precificação</td>
<td>[Informações de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>

### Ouro
{: #block_gold}

<table>
<caption>Classe de armazenamento de bloco: ouro</caption>
<thead>
<th>Características</th>
<th>Configuração</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-block-gold</code></br><code>ibmc-block-retain-gold</code></td>
</tr>
<tr>
<td>Tipo</td>
<td>[Armazenamento do Endurance](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provendurance)</td>
</tr>
<tr>
<td>Sistema de arquivos</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS por gigabyte</td>
<td>10</td>
</tr>
<tr>
<td>Intervalo de tamanho em gigabytes</td>
<td>20 - 4.000 Gi</td>
</tr>
<tr>
<td>Disco rígido</td>
<td>SSD</td>
</tr>
<tr>
<td>Faturamento</td>
<td>O tipo de faturamento padrão depende da versão de seu plug-in do {{site.data.keyword.cloud_notm}} Block Storage: <ul><li> Versão 1.0.1 e superior: por hora</li><li>Versão 1.0.0 e inferior: mensal</li></ul></td>
</tr>
<tr>
<td>Precificação</td>
<td>[Informações de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>

### Customizado
{: #block_custom}

<table>
<caption>Classe de armazenamento de bloco: customizada</caption>
<thead>
<th>Características</th>
<th>Configuração</th>
</thead>
<tbody>
<tr>
<td>Nome</td>
<td><code>ibmc-block-custom</code></br><code>ibmc-block-retain-custom</code></td>
</tr>
<tr>
<td>Tipo</td>
<td>[Desempenho](/docs/infrastructure/BlockStorage?topic=BlockStorage-About#provperformance)</td>
</tr>
<tr>
<td>Sistema de arquivos</td>
<td>ext4</td>
</tr>
<tr>
<td>IOPS e tamanho</td>
<td><strong>Intervalo de tamanho em intervalo de gigabytes/IOPS em múltiplos de 100</strong><ul><li>20-39 Gi / 100-1000 IOPS</li><li>40-79 Gi / 100-2000 IOPS</li><li>80-99 Gi / 100-4000 IOPS</li><li>100-499 Gi / 100-6000 IOPS</li><li>500-999 Gi / 100-10000 IOPS</li><li>1000-1999 Gi / 100-20000 IOPS</li><li>2000-2999 Gi / 200-40000 IOPS</li><li>3000-3999 Gi / 200-48000 IOPS</li><li>4000-7999 Gi / 300-48000 IOPS</li><li>8000-9999 Gi / 500-48000 IOPS</li><li>10000-12000 Gi / 1000-48000 IOPS</li></ul></td>
</tr>
<tr>
<td>Disco rígido</td>
<td>A razão de IOPS para gigabyte determina o tipo de disco rígido que é provisionado. Para determinar a sua razão de IOPS para gigabyte, você divide o IOPS pelo tamanho de seu armazenamento. </br></br>Exemplo: </br>Você escolheu 500 Gi de armazenamento com 100 IOPS. A sua razão é 0,2 (100 IOPS/500 Gi). </br></br><strong>Visão geral de tipos de disco rígido por razão:</strong><ul><li>Menor ou igual a 0,3: SATA</li><li>Maior que 0,3: SSD</li></ul></td>
</tr>
<tr>
<td>Faturamento</td>
<td>O tipo de faturamento padrão depende da versão de seu plug-in do {{site.data.keyword.cloud_notm}} Block Storage: <ul><li> Versão 1.0.1 e superior: por hora</li><li>Versão 1.0.0 e inferior: mensal</li></ul></td>
</tr>
<tr>
<td>Precificação</td>
<td>[Informações de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/block-storage/pricing)</td>
</tr>
</tbody>
</table>

<br />


## Classes de armazenamento customizado de amostra
{: #block_custom_storageclass}

É possível criar uma classe de armazenamento customizada e usar a classe de armazenamento no PVC.
{: shortdesc}

O {{site.data.keyword.containerlong_notm}} fornece [classes de armazenamento predefinidas](#block_storageclass_reference) para provisionar armazenamento de bloco com uma camada e configuração específicas. Em alguns casos, talvez você queira provisionar armazenamento com uma configuração diferente que não esteja coberta nas classes de armazenamento predefinidas. É possível usar os exemplos neste tópico para localizar classes de armazenamento customizadas de amostra.

Para criar sua classe de armazenamento customizada, consulte [Customizando uma classe de armazenamento](/docs/containers?topic=containers-kube_concepts#customized_storageclass). Em seguida, [use a sua classe de armazenamento customizada em seu PVC](#add_block).

### Criando armazenamento de reconhecimento de topologia
{: #topology_yaml}

Para usar o armazenamento de bloco em um cluster com múltiplas zonas, seu pod deve ser planejado na mesma zona que a sua instância de armazenamento de bloco para que seja possível ler e gravar no volume. Antes da introdução do planejamento de volume com reconhecimento de topologia pelo Kubernetes, o fornecimento dinâmico de seu armazenamento criava automaticamente a instância de armazenamento de bloco quando um PVC era criado. Em seguida, quando você criou sua pod, o planejador Kubernetes tentou implementar o pod no mesmo centro de dados que sua instância de armazenamento de bloco.
{: shortdesc}

A criação da instância de armazenamento de bloco sem saber as restrições do pod pode levar a resultados indesejados. Por exemplo, seu pod pode não estar apto a ser planejado para o mesmo nó do trabalhador que seu armazenamento porque o nó do trabalhador tem recursos insuficientes ou o nó do trabalhador está contaminado e não permite que o pod seja planejado. Com o planejamento de volume de reconhecimento de topologia, a instância de armazenamento de bloco é atrasada até que o primeiro pod que usa o armazenamento seja criado.

O planejamento de volume com reconhecimento de topologia é suportado em clusters que executam somente o Kubernetes versão 1.12 ou mais recente. Para usar esse recurso, certifique-se de ter instalado o plug-in do {{site.data.keyword.cloud_notm}} Block Storage versão 1.2.0 ou mais recente.
{: note}

Os exemplos a seguir mostram como criar classes de armazenamento que atrasem a criação da instância de armazenamento de bloco até que o primeiro pod que usa esse armazenamento esteja pronto para ser planejado. Para atrasar a criação, deve-se incluir a opção `volumeBindingMode: WaitForFirstConsumer`. Se você não incluir essa opção, o `volumeBindingMode` será configurado automaticamente como `Immediate` e a instância de armazenamento de bloco será criada quando você criar o PVC.

- ** Exemplo para armazenamento de bloco do Endurance: **
  ```
  apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: ibmc-block-bronze-delayed parameters: billingType: hourly classVersion: "2" fsType: ext4 iopsPerGB: "2" sizeRange: '[20-12000]Gi' type: Endurance provisioner: ibm.io/ibmc-block reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer
  ```
  {: codeblock}

- ** Exemplo para armazenamento de bloco de desempenho: **
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
   name: ibmc-block-performance-storageclass
   labels:
     kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-block
  parameters:
   billingType: "hourly"
   classVersion: "2"
   sizeIOPSRange: |-
     "[20-39]Gi:[100-1000]"
     "[ 40-79 ] Gi: [ 100-2000 ]"
     "[ 80-99 ] Gi: [ 100-4000 ]"
     "[ 100-499 ] Gi: [ 100-6000 ]"
     "[ 500-999 ] Gi: [ 100-10000 ]"
     "[ 1000-1999 ] Gi: [ 100-20000 ]"
     "[ 2000-2999 ] Gi: [ 200-40000 ]"
     "[ 3000-3999 ] Gi: [ 200-48000 ]"
     "[ 4000-7999 ] Gi: [ 300-48000 ]"
     "[ 8000-9999 ] Gi: [ 500-48000 ]"
     "[ 10000-12000 ] Gi: [ 1000-48000 ]"
   type: "Performance" reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer
  ```
  {: codeblock}

### Especificando a zona e a região
{: #block_multizone_yaml}

Se você deseja criar seu armazenamento de bloco em uma zona específica, será possível especificar a zona e a região em uma classe de armazenamento customizada.
{: shortdesc}

Use a classe de armazenamento customizada se você usar o plug-in {{site.data.keyword.cloud_notm}} Block Storage versão 1.0.0 ou se você desejar [provisionar estaticamente o armazenamento de bloco](#existing_block) em uma zona específica. Em todos os outros casos, [ especifique a zona diretamente em seu PVC](#add_block).
{: note}

O arquivo `.yaml` a seguir customiza uma classe de armazenamento que é baseada na classe de armazenamento sem retenção `ibm-block-silver`: o `type` é `"Endurance"`, o `iopsPerGB` é `4`, o `sizeRange` é `"[20-12000]Gi"` e o `reclaimPolicy` é configurado para `"Delete"`. A zona é especificada como `dal12`. Para usar uma classe de armazenamento diferente como sua base, consulte a [referência de classe de armazenamento](#block_storageclass_reference).

Crie a classe de armazenamento na mesma região e zona que os nós do cluster e do trabalhador. Para obter a região do seu cluster, execute `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>` e procure pelo prefixo da região na **URL principal**, como `eu-de` em `https://c2.eu-de.containers.cloud.ibm.com:11111`. Para obter a zona do seu nó do trabalhador, execute `ibmcloud oc workers --cluster <cluster_name_or_ID>`.

- ** Exemplo para armazenamento de bloco do Endurance: **
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-silver-mycustom-storageclass
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-block
  parameters:
    zone: "dal12"
    region: "us-south"
    type: "Endurance"
    iopsPerGB: "4"
    sizeRange: "[20-12000]Gi"
  reclaimPolicy: "Delete"
  ```
  {: codeblock}

- ** Exemplo para armazenamento de bloco de desempenho: **
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-performance-storageclass
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-block
  parameters:
    zone: "dal12"
    region: "us-south"
    type: "Performance"
    sizeIOPSRange: |-
      "[20-39]Gi:[100-1000]"
      "[ 40-79 ] Gi: [ 100-2000 ]"
      "[ 80-99 ] Gi: [ 100-4000 ]"
      "[ 100-499 ] Gi: [ 100-6000 ]"
      "[ 500-999 ] Gi: [ 100-10000 ]"
      "[ 1000-1999 ] Gi: [ 100-20000 ]"
      "[ 2000-2999 ] Gi: [ 200-40000 ]"
      "[ 3000-3999 ] Gi: [ 200-48000 ]"
      "[ 4000-7999 ] Gi: [ 300-48000 ]"
      "[ 8000-9999 ] Gi: [ 500-48000 ]"
      "[ 10000-12000 ] Gi: [ 1000-48000 ]"
  reclaimPolicy: "Excluir"
  ```
  {: codeblock}

### Montando o armazenamento de bloco com um sistema de arquivos `XFS`
{: #xfs}

Os exemplos a seguir criam uma classe de armazenamento que provisiona armazenamento de bloco com um sistema de arquivos `XFS`.
{: shortdesc}

- ** Exemplo para armazenamento de bloco do Endurance: **
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-block-custom-xfs
    labels:
      addonmanager.kubernetes.io/mode: Reconcile
  provisioner: ibm.io/ibmc-block
  parameters:
    type: "Endurance"
    iopsPerGB: "4"
    sizeRange: "[20-12000]Gi"
    fsType: "xfs"
  reclaimPolicy: "Delete"
  ```

- ** Exemplo para armazenamento de bloco de desempenho: **
  ```
  apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: ibmc-block-custom-xfs
     labels:
       addonmanager.kubernetes.io/mode: Reconcile
   provisioner: ibm.io/ibmc-block
   parameters:
     type: "Performance"
     sizeIOPSRange: |-
       [20-39]Gi:[100-1000]
       [40-79]Gi:[100-2000]
       [80-99]Gi:[100-4000]
       [100-499]Gi:[100-6000]
       [500-999]Gi:[100-10000]
       [1000-1999]Gi:[100-20000]
       [2000-2999]Gi:[200-40000]
       [3000-3999]Gi:[200-48000]
       [4000-7999]Gi:[300-48000]
       [8000-9999]Gi:[500-48000]
       [10000-12000]Gi:[1000-48000]
    fsType: "xfs"
     reclaimPolicy: "Delete"
     classVersion: "2"
  ```
  {: codeblock}

<br />



