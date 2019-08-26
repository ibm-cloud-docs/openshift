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

# Armazenando dados no IBM Cloud File Storage clássico
{: #file_storage}

O {{site.data.keyword.cloud_notm}} File Storage é um armazenamento de arquivo baseado em NFS persistente, rápido e conectado à rede flexível que pode ser incluído em seus apps usando volumes persistentes do Kubernetes (PVs). É possível escolher entre camadas de armazenamento predefinidas com tamanhos de GB e IOPS que atendam aos requisitos de suas cargas de trabalho. Para descobrir se o {{site.data.keyword.cloud_notm}} File Storage é a opção de armazenamento correta para você, consulte [Escolhendo uma solução de armazenamento](/docs/containers?topic=containers-storage_planning#choose_storage_solution). Para obter informações de precificação, consulte  [ Faturamento ](/docs/infrastructure/FileStorage?topic=FileStorage-about#billing).
{: shortdesc}

O {{site.data.keyword.cloud_notm}} File Storage está disponível somente para clusters padrão configurados com conectividade de rede pública. Se o seu cluster não puder acessar a rede pública, como um cluster privado atrás de um firewall ou um cluster somente com o terminal em serviço privado ativado, será possível provisionar o armazenamento de arquivo se o cluster executar o Kubernetes versão 1.13.4_1513, 1.12.6_1544, 1.11.8_1550 ou mais recente. As instâncias de armazenamento de arquivo NFS são específicas para uma única zona. Se você tiver um cluster de múltiplas zonas, considere as [opções de armazenamento persistente multizona](/docs/containers?topic=containers-storage_planning#persistent_storage_overview).
{: important}

## Decidindo sobre a configuração de armazenamento de arquivo
{: #file_predefined_storageclass}

O {{site.data.keyword.containerlong}} fornece classes de armazenamento predefinidas para armazenamento de arquivo que podem ser usadas para provisionar o armazenamento de arquivo com uma configuração específica.
{: shortdesc}

Cada classe de armazenamento especifica o tipo de armazenamento de arquivo que você provisiona, incluindo o tamanho disponível, o IOPS, o sistema de arquivos e a política de retenção.  

Depois de provisionar um tipo específico de armazenamento usando uma classe de armazenamento, não será possível mudar o tipo ou a política de retenção para o dispositivo de armazenamento. No entanto, é possível [mudar o tamanho e o IOPS](#file_change_storage_configuration) se você desejar aumentar a capacidade de armazenamento e o desempenho. Para mudar o tipo e a política de retenção para seu armazenamento, deve-se [criar uma nova instância de armazenamento e copiar os dados](/docs/containers?topic=containers-kube_concepts#update_storageclass) da instância de armazenamento antiga para a nova.
{: important}

Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

Para decidir sobre uma configuração de armazenamento:

1. Liste as classes de armazenamento disponíveis no  {{site.data.keyword.containerlong}}.
   ```
   oc get storageclasses | grep file
   ```
   {: pre}

   Saída de exemplo:
   ```
   $ oc get storageclasses
   NAME                         TYPE
   ibmc-file-bronze (default)   ibm.io/ibmc-file
   ibmc-file-custom             ibm.io/ibmc-file
   ibmc-file-gold               ibm.io/ibmc-file
   ibmc-file-retain-bronze      ibm.io/ibmc-file
   ibmc-file-retain-custom      ibm.io/ibmc-file
   ibmc-file-retain-gold        ibm.io/ibmc-file
   ibmc-file-retain-silver      ibm.io/ibmc-file
   ibmc-file-silver             ibm.io/ibmc-file
   ```
   {: screen}

2. Revise a configuração de uma classe de armazenamento.
  ```
  oc describe storageclass <storageclass_name>
  ```
  {: pre}

   Para obter mais informações sobre cada classe de armazenamento, consulte a [referência de classe de armazenamento](#file_storageclass_reference). Se você não localizar o que está procurando, considere criar a sua própria classe de armazenamento customizada. Para iniciar, consulte as [amostras de classe de armazenamento customizadas](#file_custom_storageclass).
   {: tip}

3. Escolha o tipo de armazenamento de arquivo que você deseja provisionar.
   - **Classes de armazenamento de bronze, prata e ouro:** essas classes de armazenamento provisionam o [Armazenamento do Endurance](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-endurance-tiers). O armazenamento do Endurance permite que você escolha o tamanho do armazenamento em gigabytes em camadas do IOPS predefinidas.
   - **Classe de armazenamento customizado:** essa classe de armazenamento provisiona o [Armazenamento de desempenho](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-performance). Com o armazenamento de desempenho, você tem mais controle sobre o tamanho do armazenamento e do IOPS.

4. Escolha o tamanho e o IOPS para seu armazenamento de arquivo. O tamanho e o número de IOPS definem o número total de IOPS (operações de entrada/saída por segundo) que serve como um indicador de quão rápido o seu armazenamento é. Quanto mais total de IOPS o seu armazenamento tiver, mais rápido ele processará operações de leitura e gravação.
   - **Classes de armazenamento bronze, prata e ouro:** essas classes de armazenamento vêm com um número fixo de IOPS por gigabyte e são provisionadas em discos rígidos SSD. O número total de IOPS depende do tamanho do armazenamento que você escolher. É possível selecionar qualquer número inteiro de gigabyte dentro do intervalo de tamanho permitido, como 20 Gi, 256 Gi ou 11854 Gi. Para determinar o número total de IOPS, deve-se multiplicar o IOPS com o tamanho selecionado. Por exemplo, se você selecionar um tamanho de armazenamento de arquivo de 1000Gi na classe de armazenamento prata que é fornecida com 4 IOPS por GB, seu armazenamento terá um total de 4.000 IOPS.
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
   - **Classe de armazenamento customizada:** quando você escolhe essa classe de armazenamento, tem mais controle sobre o tamanho e o IOPS desejados. Para o tamanho, é possível selecionar qualquer número inteiro de gigabyte dentro do intervalo de tamanho permitido. O tamanho que você escolher determinará o intervalo de IOPS que estará disponível para você. É possível escolher um IOPS que é um múltiplo de 100 que esteja no intervalo especificado. O IOPS que você escolhe é estático e não escala com o tamanho do armazenamento. Por exemplo, se você escolher 40 Gi com 100 IOPS, seu IOPS total permanecerá 100. </br></br> A razão de IOPS para gigabyte também determina o tipo de disco rígido que é provisionado para você. Por exemplo, se você tiver 500 Gi a 100 IOPS, a sua razão de IOPS para gigabyte será 0,2. O armazenamento com uma razão menor ou igual a 0,3 é provisionado em discos rígidos SATA. Se a sua razão for maior que 0,3, o armazenamento será provisionado em discos rígidos SSD.  
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
   - Se você desejar manter seus dados, escolha uma classe de armazenamento `retain`. Quando você exclui o PVC, somente ele é excluído. O PV, o dispositivo de armazenamento físico em sua conta de infraestrutura do IBM Cloud e seus dados ainda existem. Para recuperar o armazenamento e usá-lo em seu cluster novamente, deve-se remover o PV e seguir as etapas para [usar o armazenamento de arquivo existente](#existing_file).
   - Se desejar que o PV, os dados e seu dispositivo de armazenamento de arquivo físico sejam excluídos quando você excluir o PVC, escolha uma classe de armazenamento sem `retain`.

6. Escolha se você deseja ser faturado por hora ou mensalmente. Verifique a [precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/file-storage/pricing) para obter mais informações. Por padrão, todos os dispositivos de armazenamento de arquivo são provisionados com um tipo de faturamento por hora.
   Se você escolher um tipo de faturamento mensal, quando remover o armazenamento persistente, ainda pagará o encargo mensal por ele, mesmo que o tenha usado apenas por um curto período de tempo.
   {: note}

<br />



## Incluindo armazenamento de arquivo em apps
{: #add_file}

Crie um persistent volume claim (PVC) para [provisionar dinamicamente](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning) o armazenamento de arquivo para seu cluster. O provisionamento dinâmico cria automaticamente o volume persistente correspondente (PV) e pede o dispositivo de armazenamento físico em sua conta de infraestrutura do IBM Cloud.
{:shortdesc}

Antes de iniciar:
- Se você tiver um firewall, [permita acesso de saída](/docs/containers?topic=containers-firewall#pvc) para os intervalos de IP da infraestrutura do IBM Cloud das zonas em que seus clusters estão para que seja possível criar PVCs.
- [Decida sobre uma classe de armazenamento predefinida](#file_predefined_storageclass) ou crie uma [classe de armazenamento customizada](#file_custom_storageclass).

Procurando implementar o armazenamento de arquivo em um conjunto stateful? Veja [Usando o armazenamento de arquivo em um conjunto stateful](#file_statefulset) para obter mais informações.
{: tip}

Para incluir armazenamento de arquivo:

1.  Crie um arquivo de configuração para definir a sua solicitação de volume persistente (PVC) e salve a configuração como um arquivo `.yaml`.

    - **Exemplo para classes de armazenamento bronze, prata, ouro**:
       o arquivo `.yaml` a seguir cria uma solicitação que é denominada `mypvc` da classe de armazenamento `"ibmc-file-silver"`, faturada `"monthly"`, com um tamanho de gigabyte de `24Gi`.

       ```
       apiVersion: v1
       kind: PersistentVolumeClaim
       metadata:
         name: mypvc
         labels:
           billingType: "monthly"
           region: us-south
           zone: dal13
       spec:
         accessModes:
           - ReadWriteMany
         resources:
           requests:
             storage: 24Gi
         storageClassName: ibmc-file-silver
       ```
       {: codeblock}

    -  **Exemplo para usar a classe de armazenamento customizada**:
o arquivo `.yaml` a seguir cria uma solicitação que é denominada `mypvc` da classe de armazenamento `ibmc-file-retain-custom`, faturada `"hourly"`, com um tamanho de gigabyte de `45Gi` e IOPS de `"300"`.

       ```
       apiVersion: v1 kind: PersistentVolumeClaim metadata: name: mypvc labels: billingType: "hourly" 	 region: us-south zone: dal13 spec: accessModes:
           - ReadWriteMany
         recursos:
           pedidos:
             armazenamento: 45Gi
             iops: "300"
         storageClassName: ibmc-file-retain-custom
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
          <td>Especifique a frequência para a qual sua conta de armazenamento é calculada, como "mensal" ou "por hora". Se você não especificar um tipo de faturamento, o armazenamento será provisionado com um tipo de faturamento por hora. </td>
       </tr>
       <tr>
       <td><code> metadata.labels.region </code></td>
       <td>Opcional: especifique a região na qual você deseja provisionar seu armazenamento de arquivo. Para se conectar ao seu armazenamento, crie o armazenamento na mesma região em que seu cluster está. Se você especifica a região, deve-se também especificar uma zona. Se você não especifica uma região ou a região especificada não é localizada, o armazenamento é criado na mesma região que o seu cluster.
       </br></br>Para obter a região para seu cluster, execute `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>` e procure pelo prefixo da região na **URL principal**, como `eu-de` em `https://c2.eu-de.containers.cloud.ibm.com:11111`.
       </br></br><strong>Dica: </strong> em vez de especificar a região e a zona no PVC, também é possível especificar esses valores em uma [classe de armazenamento customizada](#file_multizone_yaml). Em seguida, use a classe de armazenamento na seção <code>metadata.annotations.volume.beta.kubernetes.io/storage-class</code> de seu PVC. Se a região e a zona forem especificadas na classe de armazenamento e no PVC, os valores no PVC terão precedência. </td>
       </tr>
       <tr>
       <td><code> metadata.labels.zone </code></td>
       <td>Opcional: especifique a zona na qual você deseja provisionar seu armazenamento de arquivo. Para usar seu armazenamento em um app, crie o armazenamento na mesma zona em que seu nó do trabalhador está. Para visualizar a zona do seu nó do trabalhador, execute <code>ibmcloud oc workers --cluster &lt;cluster_name_or_ID&gt;</code> e revise a coluna <strong>Zona</strong> de sua saída da CLI. Se você especifica a zona, deve-se também especificar uma região. Se você não especifica uma zona ou a zona especificada não é localizada em um cluster de múltiplas zonas, a zona é selecionada em uma base round-robin. </br></br><strong>Dica: </strong> em vez de especificar a região e a zona no PVC, também é possível especificar esses valores em uma [classe de armazenamento customizada](#file_multizone_yaml). Em seguida, use a classe de armazenamento na seção <code>metadata.annotations.volume.beta.kubernetes.io/storage-class</code> de seu PVC. Se a região e a zona forem especificadas na classe de armazenamento e no PVC, os valores no PVC terão precedência.
</td>
       </tr>
       <tr>
       <td><code> spec.accessMode </code></td>
       <td>Especifique uma das seguintes opções: <ul><li><strong>ReadWriteMany:</strong> o PVC pode ser montado por múltiplos pods. Todos os pods podem ler e gravar no volume. </li><li><strong>ReadOnlyMany:</strong> o PVC pode ser montado por múltiplos pods. Todos os pods têm acesso somente leitura. <li><strong>ReadWriteOnce: </strong> O PVC pode ser montado por somente um pod. Esse pod pode ler e gravar no volume. </li></ul></td>
       </tr>
       <tr>
       <td><code> spec.resources.requests.storage </code></td>
       <td>Insira o tamanho do armazenamento de arquivo, em gigabytes (Gi). Depois que seu armazenamento for provisionado, não será possível mudar o tamanho do armazenamento de arquivo. Certifique-se de especificar um tamanho que corresponda à quantia de dados que você deseja armazenar.</td>
       </tr>
       <tr>
       <td><code> spec.resources.requests.iops </code></td>
       <td>Essa opção está disponível somente para as classes de armazenamento customizadas (`ibmc-file-custom/ibmc-file-retain-custom`). Especifique o IOPS total para o armazenamento, selecionando um múltiplo de 100 dentro do intervalo permitido. Se você escolher um IOPS diferente de um que esteja listado, o IOPS será arredondado para cima.</td>
       </tr>
       <tr>
       <td><code> spec.storageClassName </code></td>
       <td>O nome da classe de armazenamento que você deseja usar para provisionar armazenamento de arquivo. É possível optar por usar uma das [classes de armazenamento fornecidas pela IBM](#file_storageclass_reference) ou [criar a sua própria](#file_custom_storageclass). </br> Se você não especificar uma classe de armazenamento, o PV será criado com a classe de armazenamento padrão <code>ibmc-file-bronze</code>. </br></br><strong>Dica:</strong> se você desejar mudar a classe de armazenamento padrão, execute <code>oc patch storageclass &lt;storageclass&gt; -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'</code> e substitua <code>&lt;storageclass&gt;</code> pelo nome da classe de armazenamento.</td>
       </tr>
       </tbody></table>

    Se você deseja usar uma classe de armazenamento customizado, crie seu PVC com o nome de classe de armazenamento correspondente, um IOPS válido e o tamanho.   
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
    Access Modes:	RWX
    Events:
      FirstSeen	LastSeen	Count	From								SubObjectPath	Type		Reason			Message
      ---------	--------	-----	----								-------------	--------	------			-------
      3m		3m		1	{ibm.io/ibmc-file 31898035-3011-11e7-a6a4-7a08779efd33 }			Normal		Provisioning		External provisioner is provisioning volume for claim "default/my-persistent-volume-claim"
      3m		1m		10	{persistentvolume-controller }							Normal		ExternalProvisioning	cannot find provisioner "ibm.io/ibmc-file", expecting that a volume for the claim is provisioned either manually or via external software
      1m		1m		1	{ibm.io/ibmc-file 31898035-3011-11e7-a6a4-7a08779efd33 }			Normal		ProvisioningSucceeded	Successfully provisioned volume pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2

    ```
    {: screen}

4.  {: #file_app_volume_mount}Para montar o armazenamento em sua implementação, crie um arquivo de configuração `.yaml` e especifique o PVC que liga o PV.

    Se você tiver um app que requer que um usuário não raiz grave no armazenamento persistente ou um app que requer que o caminho de montagem seja de propriedade do usuário raiz, consulte [Incluindo acesso de usuário não raiz no armazenamento de arquivo NFS](/docs/containers?topic=containers-cs_troubleshoot_storage#nonroot) ou [Ativando a permissão raiz para armazenamento de arquivo NFS](/docs/containers?topic=containers-cs_troubleshoot_storage#nonroot).
    {: tip}

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
    <td>O caminho absoluto do diretório no qual o volume está montado dentro do contêiner. Os dados que são gravados no caminho de montagem são armazenados sob o diretório <code>root</code> em sua instância de armazenamento de arquivo físico. Se você desejar compartilhar um volume entre apps diferentes, será possível especificar [subcaminhos do volume ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath) para cada um de seus apps.  </td>
    </tr>
    <tr>
    <td><code> spec.containers.volumeMounts.name </code></td>
    <td>O nome do volume a ser montado no pod.</td>
    </tr>
    <tr>
    <td><code> volumes.name </code></td>
    <td>O nome do volume a ser montado no pod. Geralmente, esse nome é igual a <code>volumeMounts.name</code>.</td>
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


## Usando armazenamento de arquivo existente em seu cluster
{: #existing_file}

Se você tiver um dispositivo de armazenamento físico existente que desejar usar em seu cluster, será possível criar manualmente o PV e o PVC para [provisionar estaticamente](/docs/containers?topic=containers-kube_concepts#static_provisioning) o armazenamento.
{: shortdesc}

Antes de iniciar:
- Certifique-se de que você tenha pelo menos um nó do trabalhador que exista na mesma zona que sua instância de armazenamento de arquivo existente.
- [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

### Etapa 1: Preparando seu armazenamento existente.
{: #existing-file-1}

Para que seja possível iniciar a montagem de seu armazenamento existente em um app, deve-se recuperar todas as informações necessárias para seu PV e preparar o armazenamento para ser acessível em seu cluster.  
{: shortdesc}

**Para o armazenamento provisionado com uma classe de armazenamento `retain`:** </br>
se você provisionou um armazenamento com uma classe de armazenamento `retain` e remover a PVC, o PV e o dispositivo de armazenamento físico não serão removidos automaticamente. Para reutilizar o armazenamento em seu cluster, deve-se remover o PV restante primeiro.

Para usar o armazenamento existente em um cluster diferente daquele em que você o provisionou, siga as etapas para [armazenamento que foi criado fora do cluster](#external_storage) para incluir o armazenamento na sub-rede de seu nó do trabalhador.
{: tip}

1. Liste PVs existentes.
   ```
   oc get pv
   ```
   {: pre}

   Procure o PV que pertence ao seu armazenamento persistente. O PV está em um estado `released`.

2. Obter os detalhes do PV.
   ```
   oc describe pv <pv_name>
   ```
   {: pre}

3. Observe o `CapacityGb`, `storageClass`, `failure-domain.beta.kubernetes.io/region`, `failure-domain.beta.kubernetes.io/zone`, `server` e `path`.

4. Remova o PV.
   ```
   oc delete pv <pv_name>
   ```
   {: pre}

5. Verifique se o PV foi removido.
   ```
   oc get pv
   ```
   {: pre}

</br>

**Para o armazenamento persistente provisionado fora do cluster:** </br>
Se desejar usar um armazenamento existente provisionado anteriormente, mas nunca usado em seu cluster, deverá disponibilizá-lo na mesma sub-rede de seus nós do trabalhador.

1.  {: #external_storage}No [Portal de infraestrutura do IBM Cloud ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/classic?), clique em **Armazenamento**.
2.  Clique em **File Storage** e, no menu **Ações**, selecione **Autorizar host**.
3.  Selecione **Subnets**.
4.  Na lista suspensa, selecione a sub-rede VLAN privada à qual o seu nó do trabalhador está conectado. Para localizar a sub-rede do seu nó do trabalhador, execute `ibmcloud oc workers --cluster <cluster_name>` e compare o `Private IP` do seu nó do trabalhador com a sub-rede que você localizou na lista suspensa.
5.  Clique em **Enviar**.
6.  Clique no nome do armazenamento de arquivo.
7.  Observe o `Mount Point`, o `size` e o campo `Location`. O campo `Mount Point` é exibido como `<nfs_server>:<file_storage_path>`.

### Etapa 2: Criando um volume persistente (PV) e uma solicitação de volume persistente correspondente (PVC)
{: #existing-file-2}

1.  Crie um arquivo de configuração de armazenamento para seu PV. Inclua os valores que você recuperou anteriormente.

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
       storage: "<size>"
     accessModes:
       - ReadWriteMany
     nfs:
       server: "<nfs_server>"
       path: "<file_storage_path>"
    ```
    {: codeblock}

    <table>
    <caption>Entendendo os componentes de arquivo YAML</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Ícone de ideia"/> entendendo os componentes de arquivo do YAML</th>
    </thead>
    <tbody>
    <tr>
    <td><code>name</code></td>
    <td>Insira o nome do objeto PV a ser criado.</td>
    </tr>
    <tr>
    <td><code>metadata.labels</code></td>
    <td>Insira a região e a zona que você recuperou anteriormente. Deve-se ter pelo menos um nó do trabalhador na mesma região e zona que o seu armazenamento persistente para montar o armazenamento em seu cluster. Se um PV para o seu armazenamento já existir, [inclua o rótulo de zona e região](/docs/containers?topic=containers-kube_concepts#storage_multizone) em seu PV.
    </tr>
    <tr>
    <td><code> spec.capacity.storage </code></td>
    <td>Insira o tamanho de armazenamento do compartilhamento de arquivo NFS existente que você recuperou anteriormente. O tamanho de armazenamento deve ser gravado em gigabytes, por exemplo, 20Gi (20 GB) ou 1000Gi (1 TB), e o tamanho deve corresponder ao tamanho do compartilhamento de arquivo existente.</td>
    </tr>
    <tr>
    <td><code> spec.accessMode </code></td>
    <td>Especifique uma das seguintes opções: <ul><li><strong>ReadWriteMany:</strong> o PVC pode ser montado por múltiplos pods. Todos os pods podem ler e gravar no volume. </li><li><strong>ReadOnlyMany:</strong> o PVC pode ser montado por múltiplos pods. Todos os pods têm acesso somente leitura. <li><strong>ReadWriteOnce: </strong> O PVC pode ser montado por somente um pod. Esse pod pode ler e gravar no volume. </li></ul></td>
    </tr>
    <tr>
    <td><code> spec.nfs.server </code></td>
    <td>Insira o ID do servidor de compartilhamento de arquivo NFS que você recuperou anteriormente.</td>
    </tr>
    <tr>
    <td><code>path</code></td>
    <td>Insira o caminho para o compartilhamento de arquivo NFS que você recuperou anteriormente.</td>
    </tr>
    </tbody></table>

3.  Crie o PV em seu cluster.

    ```
    oc apply -f mypv.yaml
    ```
    {: pre}

4.  Verifique se o PV é criado.

    ```
    oc get pv
    ```
    {: pre}

5.  Crie outro arquivo de configuração para criar seu PVC. Para que o PVC corresponda ao PV criado anteriormente, deve-se escolher o mesmo valor para `storage` e `accessMode`. O campo `storage-class` deve estar vazio. Se algum desses campos não corresponder ao PV, um novo PV e uma nova instância de armazenamento físico serão [provisionados dinamicamente](/docs/containers?topic=containers-kube_concepts#dynamic_provisioning).

    ```
    kind: PersistentVolumeClaim apiVersion: v1 metadata: name: mypvc spec: accessModes:
       - ReadWriteMany
     resources:
       requests:
         storage: "<size>"
     storageClassName:
    ```
    {: codeblock}

6.  Crie seu PVC.

    ```
    oc apply -f mypvc.yaml
    ```
    {: pre}

7.  Verifique se o PVC foi criado e ligado ao PV. Esse processo pode levar alguns minutos.

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
    Access Modes: RWX
    Events:
      FirstSeen LastSeen Count From        SubObjectPath Type Reason Message
      --------- -------- ----- ----        ------------- -------- ------ -------
      3m 3m 1 {ibm.io/ibmc-file 31898035-3011-11e7-a6a4-7a08779efd33 } Normal Provisioning External provisioner is provisioning volume for claim "default/my-persistent-volume-claim"
      3m 1m	 10 {persistentvolume-controller } Normal ExternalProvisioning cannot find provisioner "ibm.io/ibmc-file", expecting that a volume for the claim is provisioned either manually or via external software
      1m 1m 1 {ibm.io/ibmc-file 31898035-3011-11e7-a6a4-7a08779efd33 } Normal ProvisioningSucceeded	Successfully provisioned volume pvc-0d787071-3a67-11e7-aafc-eef80dd2dea2
    ```
    {: screen}


Você criou com êxito um PV e ligou-o a um PVC. Os usuários do cluster agora podem [montar o PVC](#file_app_volume_mount) para suas implementações e começar a ler e gravar no objeto PV.

<br />



## Usando o armazenamento de arquivo em um conjunto stateful
{: #file_statefulset}

Se você tiver um app stateful como um banco de dados, será possível criar conjuntos stateful que usam armazenamento de arquivo para armazenar os dados de seu app. Como alternativa, é possível usar um banco de dados como um serviço do {{site.data.keyword.cloud_notm}} e armazenar seus dados na nuvem.
{: shortdesc}

**De que eu preciso estar ciente ao incluir armazenamento de arquivo em um conjunto stateful?** </br>
Para incluir armazenamento em um conjunto stateful, especifique sua configuração de armazenamento na seção `volumeClaimTemplates` do YAML do conjunto stateful. O `volumeClaimTemplates` é a base para seu PVC e pode incluir a classe de armazenamento e o tamanho ou IOPS do armazenamento de arquivo que você deseja provisionar. No entanto, se você desejar incluir rótulos nos `volumeClaimTemplates`, os Kubernetes não incluirão esses rótulos ao criar o PVC. Em vez disso, deve-se incluir os rótulos diretamente no conjunto stateful.

Não é possível implementar dois conjuntos stateful ao mesmo tempo. Se você tentar criar um conjunto stateful antes que um diferente seja totalmente implementado, a implementação do conjunto stateful poderá levar a resultados inesperados.
{: important}

**Como posso criar meu conjunto stateful em uma zona específica?** </br>
Em um cluster com várias zonas, é possível especificar a zona e a região em que você deseja criar seu conjunto stateful nas seções `spec.selector.matchLabels` e `spec.template.metadata.labels` do YAML do conjunto stateful. Como alternativa, é possível incluir esses rótulos em uma [classe de armazenamento customizada](/docs/containers?topic=containers-kube_concepts#customized_storageclass) e usar essa classe de armazenamento na seção `volumeClaimTemplates` de seu conjunto stateful.

**Posso atrasar a ligação de um PV ao meu pod stateful até que o pod esteja pronto?**<br>
Sim, é possível [criar uma classe de armazenamento customizada](#file-topology) para seu PVC que inclui o campo [`volumeBindingMode: WaitForFirstConsumer` ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode).

**Quais opções eu tenho para incluir armazenamento de arquivo em um conjunto stateful?** </br>
Se você desejar criar automaticamente seu PVC ao criar o conjunto stateful, use o [fornecimento dinâmico](#file_dynamic_statefulset). Também é possível optar por [pré-provisionar os PVCs ou usar PVCs existentes](#file_static_statefulset) com o conjunto stateful.  

### Fornecimento dinâmico: criando o PVC ao criar um conjunto stateful
{: #file_dynamic_statefulset}

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

    O exemplo a seguir mostra como implementar o NGINX como um conjunto stateful com 3 réplicas. Para cada réplica, um dispositivo de armazenamento de arquivo de 20 gigabyte é fornecido com base nas especificações na classe de armazenamento `ibmc-file-retain-bronze`. Todos os dispositivos de armazenamento são provisionados na zona `dal10`. Como o armazenamento de arquivo não pode ser acessado de outras zonas, todas as réplicas do conjunto stateful também são implementadas nos nós do trabalhador que estão localizados em `dal10`.

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
         storageClassName: ibmc-file-retain-bronze
    ```
    {: codeblock}

  - **Exemplo de conjunto stateful com a regra de antiafinidade e a criação de armazenamento de arquivo atrasada:**

    O exemplo a seguir mostra como implementar o NGINX como um conjunto stateful com 3 réplicas. O conjunto stateful não especifica a região e a zona em que o armazenamento de arquivo é criado. Em vez disso, o conjunto stateful usa uma regra de antiafinidade para assegurar que os pods sejam difundidos entre os nós do trabalhador e as zonas. A antiafinidade do nó do trabalhador é obtida definindo o rótulo `app: nginx`. Esse rótulo instrui o planejador do Kubernetes a não planejar um pod em um nó do trabalhador se um pod com o mesmo rótulo já estiver em execução nesse nó do trabalhador. O rótulo `topologykey: failure-domain.beta.kubernetes.io/zone` restringe essa regra de antiafinidade ainda mais e evita que o pod seja planejado em um nó do trabalhador que está localizado na mesma zona que um nó do trabalhador que já executa um pod com o rótulo `app: nginx`. Para cada pod do conjunto stateful, dois PVCs são criados conforme definidos na seção `volumeClaimTemplates`, mas a criação das instâncias de armazenamento de arquivo é atrasada até que um pod do conjunto stateful que use o armazenamento seja planejado. Essa configuração é referida como [planejamento de volume com reconhecimento de topologia](https://kubernetes.io/blog/2018/10/11/topology-aware-volume-provisioning-in-kubernetes/).

    ```
    apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: ibmc-file-bronze-delayed parameters: billingType: hourly classVersion: "2" iopsPerGB: "2" sizeRange: '[20-12000]Gi' type: Endurance provisioner: ibm.io/ibmc-file reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer
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
          - ReadWriteMany # access mode resources: requests: storage: 20Gi storageClassName: ibmc-file-bronze-delayed
      - metadata: name: myvol2 spec: accessModes:
          - ReadWriteMany # access mode resources: requests: storage: 20Gi storageClassName: ibmc-file-bronze-delayed
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
    <td style="text-align:left">Insira a política de gerenciamento de pod que deseja usar para o conjunto stateful. Escolha entre as opções a seguir: <ul><li><strong><code>OrderedReady</code></strong>: Com essa opção, as réplicas do conjunto stateful são implementadas uma após a outra. Por exemplo, se você tiver especificado 3 réplicas, o Kubernetes criará o PVC para sua primeira réplica, aguardará até que o PVC seja ligado, implementará a réplica do conjunto stateful e montará o PVC para a réplica. Depois que a implementação é concluída, a segunda réplica é implementada. Para obter mais informações sobre essa opção, consulte [Gerenciamento de pod `OrderedReady` ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#orderedready-pod-management). </li><li><strong>Paralelo: </strong> com essa opção, a implementação de todas as réplicas do conjunto stateful é iniciada ao mesmo tempo. Se o seu app suportar a implementação paralela de réplicas, use essa opção para economizar tempo de implementação para seus PVCs e réplicas do conjunto stateful. </li></ul></td>
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
    <td style="text-align:left">Insira o tamanho do armazenamento de arquivo em gigabytes (Gi).</td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.spec.resources.</code></br><code>requests.iops</code></td>
    <td style="text-align:left">Se você desejar fornecer o [armazenamento de desempenho](#file_predefined_storageclass), insira o número de IOPS. Se você usar uma classe de armazenamento do Endurance e especificar vários IOPS, o número de IOPS será ignorado. Em vez disso, o IOPS especificado em sua classe de armazenamento é usado.  </td>
    </tr>
    <tr>
    <td style="text-align:left"><code>spec.volumeClaimTemplates.</code></br><code>spec.storageClassName</code></td>
    <td style="text-align:left">Insira a classe de armazenamento que deseja usar. Para listar classes de armazenamento existentes, execute <code>oc get storageclasses | grep file</code>. Se você não especificar uma classe de armazenamento, o PVC será criado com a classe de armazenamento padrão configurada em seu cluster. Certifique-se de que a classe de armazenamento padrão use o provisionador <code>ibm.io/ibmc-file</code> para que seu conjunto stateful seja provisionado com armazenamento de arquivo.</td>
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

### Fornecimento estático: usando um PVC existente com seu conjunto stateful
{: #file_static_statefulset}

É possível pré-provisionar seus PVCs antes de criar seu conjunto stateful ou usar PVCs existentes com esse conjunto.
{: shortdesc}

Quando você [provisionar dinamicamente seus PVCs ao criar o conjunto stateful](#file_dynamic_statefulset), o nome do PVC será designado com base nos valores usados no arquivo YAML do conjunto stateful. Para que o conjunto stateful use PVCs existentes, o nome dos PVCs deve corresponder ao nome que seria criado automaticamente ao usar o fornecimento dinâmico.

Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Se você desejar pré-fornecer seu PVC antes de criar o conjunto stateful, siga as etapas de 1 a 3 em [Incluindo armazenamento de arquivo em apps](#add_file) para criar um PVC para cada réplica do conjunto stateful. Certifique-se de criar sua PVC com um nome que siga o formato a seguir: `<volume_name>-<statefulset_name>-<replica_number>`.
   - **`<volume_name>`**: use o nome que você deseja especificar na seção `spec.volumeClaimTemplates.metadata.name` de seu conjunto stateful, como `nginxvol`.
   - **`<statefulset_name>`**: use o nome que você deseja especificar na seção `metadata.name` de seu conjunto stateful, como `nginx_statefulset`.
   - **`<replica_number>`**: insira o número de sua réplica começando em 0.

   Por exemplo, se for necessário criar 3 réplicas do conjunto stateful, crie 3 PVCs com os nomes a seguir: `nginxvol-nginx_statefulset-0`, `nginxvol-nginx_statefulset-1` e `nginxvol-nginx_statefulset-2`.  

   Procurando criar um PVC e um PV para uma instância de armazenamento de arquivo existente? Crie seu PVC e PV usando o [fornecimento estático](#existing_file).
   {: tip}

2. Siga as etapas em [Fornecimento dinâmico: criando o PVC ao criar um conjunto stateful](#file_dynamic_statefulset) para criar seu conjunto stateful. O nome de sua PVC segue o formato `<volume_name>-<statefulset_name>-<replica_number>`. Certifique-se de usar os valores a seguir de seu nome do PVC na especificação do conjunto stateful:
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
{: #file_change_storage_configuration}

Se você desejar aumentar a capacidade de armazenamento ou o desempenho, será possível modificar seu volume existente.
{: shortdesc}

Para perguntas sobre faturamento e para localizar as etapas de como usar o console do {{site.data.keyword.cloud_notm}} para modificar seu armazenamento, veja [Expandir capacidade de compartilhamento de arquivo](/docs/infrastructure/FileStorage?topic=FileStorage-expandCapacity#expandCapacity).
{: tip}

1. Liste os PVCs em seu cluster e anote o nome do PV associado na coluna **VOLUME**.
   ```
   oc get pvc
   ```
   {: pre}

   Saída de exemplo:
   ```
   NAME             STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS        AGE
   myvol            Bound     pvc-01ac123a-123b-12c3-abcd-0a1234cb12d3   20Gi       RWX            ibmc-file-bronze    147d
   ```
   {: screen}

2. Recupere o **`StorageType`**, o **`volumeId`** e o **`servidor`** do armazenamento de arquivo físico que está associado ao seu PVC, listando os detalhes do PV ao qual o PVC está ligado. Substitua `<pv_name>` pelo nome do PV recuperado na etapa anterior. O tipo de armazenamento, o ID do volume e o nome do servidor são mostrados na seção **`Rótulos`** de sua saída da CLI.
   ```
   oc describe pv <pv_name>
   ```
   {: pre}

   Saída de exemplo:
   ```
   Name:            pvc-4b62c704-5f77-11e8-8a75-b229c11ba64a
   Labels:          CapacityGb=20
                    Datacenter=dal10
                    Iops=2
                    StorageType=ENDURANCE
                    Username=IBM02SEV1543159_6
                    billingType=hourly
                    failure-domain.beta.kubernetes.io/region=us-south
                    failure-domain.beta.kubernetes.io/zone=dal10
                    path=IBM01SEV1234567_8ab12t
                    server=fsf-dal1001g-fz.adn.networklayer.com
                    volumeId=12345678
   ...
   ```
   {: screen}

3. Modifique o tamanho ou o IOPS de seu volume em sua conta de infraestrutura do IBM Cloud.

   Exemplo para armazenamento de desempenho:
   ```
   ibmcloud sl file volume-modify <volume_ID> --new-size <size> --new-iops <iops>
   ```
   {: pre}

   Exemplo para armazenamento do Endurance:
   ```
   ibmcloud sl file volume-modify <volume_ID> --new-size <size> --new-tier <iops>
   ```
   {: pre}

   <table>
   <caption>Entendendo os componentes do comando</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Ícone de ideia"/> entendendo os componentes de arquivo do YAML</th>
   </thead>
   <tbody>
   <tr>
   <td><code>&lt;volume_ID&gt;</code></td>
   <td>Insira o ID do volume recuperado anteriormente.</td>
   </tr>
   <tr>
   <td><code>&lt;new-size&gt;</code></td>
   <td>Insira o novo tamanho em gigabytes (Gi) para seu volume. Para tamanhos válidos, consulte [Decidindo sobre a configuração de armazenamento de arquivo](#file_predefined_storageclass). O tamanho inserido deve ser maior ou igual ao tamanho atual de seu volume. Se você não especificar um novo tamanho, o tamanho atual do volume será usado. </td>
   </tr>
   <tr>
   <td><code>&lt;new-iops&gt;</code></td>
   <td>Somente para armazenamento de desempenho. Insira o novo número de IOPS que você deseja. Para o IOPS válido, consulte [Decidindo sobre a configuração de armazenamento de arquivo](#file_predefined_storageclass). Se você não especificar o IOPS, o IOPS atual será usado. <p class="note">Se a razão IOPS/GB original para o volume for menor que 0,3, a nova razão IOPS/GB deverá ser menor que 0,3. Se a razão IOPS/GB original para o volume for maior ou igual a 0,3, a nova razão IOPS/GB para o volume deverá ser maior ou igual a 0,3.</p> </td>
   </tr>
   <tr>
   <td><code>&lt;new-tier&gt;</code></td>
   <td>Somente para armazenamento do Endurance. Insira o novo número de IOPS por GB que você deseja. Para o IOPS válido, consulte [Decidindo sobre a configuração de armazenamento de arquivo](#file_predefined_storageclass). Se você não especificar o IOPS, o IOPS atual será usado. <p class="note">Se a razão IOPS/GB original para o volume for menor que 0,25, a nova razão IOPS/GB deverá ser menor que 0,25. Se a razão IOPS/GB original para o volume for maior ou igual a 0,25, a nova razão IOPS/GB para o volume deverá ser maior ou igual a 0,25.</p> </td>
   </tr>
   </tbody>
   </table>

   Saída de exemplo:
   ```
   Order 31020713 was placed successfully!.
   > Storage as a Service

   > 40 GBs

   > 2 IOPS per GB

   > 20 GB de espaço de armazenamento (Espaço de captura instantânea)

   You may run 'ibmcloud sl file volume-list --order 12345667' to find this file volume after it is ready.
   ```
   {: screen}

4. Se você mudou o tamanho de seu volume e usa o volume em um pod, efetue login em seu pod para verificar o novo tamanho.
   1. Liste todos os pods que usam PVC.
      ```
      oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.persistentVolumeClaim.claimName}{" "}{end}{end}' | grep "<pvc_name>"
      ```
      {: pre}

      Pods são retornados no formato: `<pod_name>: <pvc_name>`.
   2. Efetue login em seu pod.
      ```
      oc exec -it <pod_name> bash
      ```
      {: pre}

   3. Mostre as estatísticas de uso do disco e localize o caminho do servidor para seu volume que você recuperou anteriormente.
      ```
      df -h
      ```
      {: pre}

      Saída de exemplo:
      ```
      Filesystem                                                      Size  Used Avail Use% Mounted on
      overlay                                                          99G  4.8G   89G   6% /
      tmpfs                                                            64M     0   64M   0% /dev
      tmpfs                                                           7.9G     0  7.9G   0% /sys/fs/cgroup
      fsf-dal1001g-fz.adn.networklayer.com:/IBM01SEV1234567_6/data01   40G     0   40G   0% /myvol
      ```
      {: screen}


## Mudando a versão do NFS padrão
{: #nfs_version}

A versão do armazenamento de arquivo determina o protocolo que é usado para se comunicar com o servidor de armazenamento de arquivo do {{site.data.keyword.cloud_notm}}. Por padrão, todas as instâncias de armazenamento de arquivo são configuradas com o NFS versão 4. É possível mudar o PV existente para uma versão mais antiga do NFS se seu app requer uma versão específica para funcionar adequadamente.
{: shortdesc}

Para mudar a versão do NFS padrão, é possível criar uma nova classe de armazenamento para provisionar o armazenamento de arquivo dinamicamente em seu cluster ou escolher mudar um PV existente que é montado em seu pod.

Para aplicar as atualizações de segurança mais recentes e para um melhor desempenho, use a versão do NFS padrão e não mude para uma versão mais antiga do NFS.
{: important}

**Para criar uma classe de armazenamento customizada com uma versão do NFS específica:**
1. Crie uma [classe de armazenamento customizada](#nfs_version_class) com a versão do NFS que você deseja provisionar.
2. Crie a classe de armazenamento em seu cluster.
   ```
   oc apply -f nfsversion_storageclass.yaml
   ```
   {: pre}

3. Verifique se a classe de armazenamento customizado foi criada.
   ```
   oc get storageclasses
   ```
   {: pre}

4. Provisione o [armazenamento de arquivo](#add_file) com sua classe de armazenamento customizada.

**Para mudar seu PV existente para usar uma versão diferente do NFS:**

1. Obtenha o PV do armazenamento de arquivo no qual você deseja mudar a versão do NFS e anote o nome do PV.
   ```
   oc get pv
   ```
   {: pre}

2. Inclua uma anotação em seu PV. Substitua `<version_number>` pela versão do NFS que deseja usar. Por exemplo, para mudar para o NFS versão 3.0, insira **3**.  
   ```
   oc patch pv <pv_name> -p '{"metadata": {"annotations":{"volume.beta.kubernetes.io/mount-options":"vers=<version_number>"}}}'
   ```
   {: pre}

3. Exclua o pod que usa o armazenamento de arquivos e recrie o pod.
   1. Salve o YAML do pod em sua máquina local.
      ```
      kubect get pod <pod_name> -o yaml > <filepath/pod.yaml>
      ```
      {: pre}

   2. Exclua o pod.
      ```
      oc deleted pod <pod_name>
      ```
      {: pre}

   3. Recrie o pod.
      ```
      oc apply -f pod.yaml
      ```
      {: pre}

4. Aguarde o pod para implementar.
   ```
   oc get pods
   ```
   {: pre}

   O pod é totalmente implementado quando o status muda para `Running`.

5. Efetue login em seu pod.
   ```
   oc exec -it <pod_name> sh
   ```
   {: pre}

6. Verifique se o armazenamento de arquivo foi montado com a versão do NFS que você especificou anteriormente.
   ```
   mount | grep "nfs" | awk -F" |," '{ print $5, $8 }'
   ```
   {: pre}

   Saída de exemplo:
   ```
   Nfs vers=3.0
   ```
   {: screen}

<br />


## Fazendo backup e restaurando dados
{: #file_backup_restore}

O armazenamento de arquivo é provisionado no mesmo local que os nós do trabalhador em seu cluster. O armazenamento é hospedado em servidores em cluster pela IBM para fornecer disponibilidade no caso de um servidor ficar inativo. No entanto, o armazenamento de arquivo não será submetido a backup automaticamente e poderá ser inacessível se o local inteiro falhar. Para proteger seus dados contra perda ou danos, será possível configurar backups periódicos que poderão ser usados para restaurar seus dados quando necessário.
{: shortdesc}

Revise as opções de backup e restauração a seguir para o seu armazenamento de arquivo:

<dl>
  <dt>Configurar capturas instantâneas periódicas</dt>
  <dd><p>É possível [configurar capturas instantâneas periódicas para o seu armazenamento de arquivo](/docs/infrastructure/FileStorage?topic=FileStorage-snapshots), que é uma imagem somente leitura que captura o estado da instância em um momento. Para armazenar a captura instantânea, deve-se solicitar espaço de captura instantânea em seu armazenamento de arquivo. As capturas instantâneas são armazenadas na instância de armazenamento existente dentro da mesma zona. Será possível restaurar dados de uma captura instantânea se um usuário acidentalmente remover dados importantes do volume.</br> <strong>Para criar uma captura instantânea para seu volume: </strong><ol><li>[Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)</li><li>Efetue login na CLI `ibmcloud sl`. <pre class="pre"><code>    ibmcloud sl init
    </code></pre></li><li>PVs de Lista existente em seu cluster. <pre class="pre"><code>oc get pv</code></pre></li><li>Obtenha os detalhes para o PV para o qual você deseja criar espaço de captura instantânea e anote o ID do volume, o tamanho e os IOPS. <pre class="pre"><code>oc describe pv &lt;pv_name&gt;</code></pre> O ID do volume, o tamanho e o IOPS podem ser localizados na seção <strong>Labels</strong> de sua saída da CLI. </li><li>Crie o tamanho da captura instantânea para o volume existente com os parâmetros que você recuperou na etapa anterior. <pre class="pre"><code>ibmcloud sl file snapshot-order &lt;volume_ID&gt; --size &lt;size&gt; --tier &lt;iops&gt;</code></pre></li><li>Espere o tamanho da captura instantânea para criar. <pre class="pre"><code> ibmcloud sl arquivo volume-detail  &lt;volume_ID&gt; </code></pre>O tamanho da captura instantânea é provisionado com êxito quando o <strong>Tamanho da captura instantânea (GB)</strong> na saída da CLI muda de 0 para o tamanho solicitado. </li><li>Crie a captura instantânea para o volume e anote o ID da captura instantânea que é criado para você. <pre class="pre"><code> Captura instantânea do arquivo ibmcloud sl-create  &lt;volume_ID&gt; </code></pre></li><li>Verifique se a captura instantânea foi criada com êxito. <pre class="pre"><code> ibmcloud sl file snapshot-list  &lt;volume_ID&gt; </code></pre></li></ol></br><strong>Para restaurar dados por meio de uma captura instantânea para um volume existente: </strong><pre class="pre"><code> ibmcloud sl file snapshot-restore  &lt;volume_ID&gt;  &lt;snapshot_ID&gt; </code></pre></p></dd>
  <dt>Replicar capturas instantâneas para outra zona</dt>
 <dd><p>Para proteger seus dados de uma falha de zona, é possível [replicar capturas instantâneas](/docs/infrastructure/FileStorage?topic=FileStorage-replication#replication) para uma instância de armazenamento de arquivo que está configurada em outra zona. Os dados podem ser replicados do armazenamento primário para o armazenamento de backup somente. Não é possível montar uma instância de armazenamento de arquivo replicada em um cluster. Quando seu armazenamento primário falha, é possível configurar manualmente o armazenamento de backup replicado para ser o primário. Em seguida, é possível montá-lo para seu cluster. Depois que o armazenamento primário é restaurado, é possível restaurar os dados do armazenamento de backup.</p></dd>
 <dt>Armazenamento duplicado</dt>
 <dd><p>É possível [duplicar sua instância de armazenamento de arquivo](/docs/infrastructure/FileStorage?topic=FileStorage-duplicatevolume#duplicatevolume) na mesma zona que a instância de armazenamento original. Uma duplicata tem os mesmos dados que a instância de armazenamento original no momento em que é criada. Diferentemente de réplicas, use a duplicata como uma instância de armazenamento independente da original. Para duplicar, primeiro [configure capturas instantâneas para o volume](/docs/infrastructure/FileStorage?topic=FileStorage-snapshots).</p></dd>
  <dt>Faça backup dos dados para {{site.data.keyword.cos_full}}</dt>
  <dd><p>É possível usar a [**imagem ibm-backup-restore**](/docs/services/RegistryImages/ibm-backup-restore?topic=RegistryImages-ibmbackup_restore_starter#ibmbackup_restore_starter) para ativar um backup e restaurar o pod em seu cluster. Esse pod contém um script para executar um backup único ou periódico para qualquer persistent volume claim (PVC) em seu cluster. Os dados são armazenados em sua instância do {{site.data.keyword.cos_full}} que você configurou em uma zona.</p>
  <p>Para tornar os seus dados ainda mais altamente disponíveis e proteger o seu app de uma falha de zona, configure uma segunda instância do {{site.data.keyword.cos_full}} e replique dados entre as zonas. Se você precisa restaurar dados de sua instância do {{site.data.keyword.cos_full}}, use o script de restauração que é fornecido com a imagem.</p></dd>
<dt>Copiar dados de e para pods e contêineres</dt>
<dd><p>É possível usar o [comando![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/reference/kubectl/overview/#cp) `oc cp` para copiar arquivos e diretórios para e por meio de pods ou contêineres específicos em seu cluster.</p>
<p>Antes de iniciar: [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Se você não especificar um contêiner com <code>-c</code>, o comando usará o primeiro contêiner disponível no pod.</p>
<p>É possível usar o comando de várias maneiras:</p>
<ul>
<li>Copie dados de sua máquina local para um pod em seu cluster:<pre class="pre"><code>oc cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var></code></pre></li>
<li>Copie dados de um pod em seu cluster para sua máquina local: <pre class="pre"><code>oc cp <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;/&lt;filename&gt;</var> <var>&lt;local_filepath&gt;/&lt;filename&gt;</var></code></pre></li>
<li>Copiar dados de sua máquina local para um contêiner específico que é executado em um pod em seu cluster: <pre class="pre"><code>oc cp <var>&lt;local_filepath&gt;/&lt;filename&gt;</var> <var>&lt;namespace&gt;/&lt;pod&gt;:&lt;pod_filepath&gt;</var> -c <var>&lt;container></var></code></pre></li>
</ul></dd>
  </dl>

<br />


## Referência de classe de armazenamento
{: #file_storageclass_reference}

| Características | Configuração|
|:-----------------|:-----------------|
| Nome | <code>ibmc-file-bronze</code></br><code>ibmc-file-retain-bronze</code>|
| Tipo | [Armazenamento do Endurance](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-endurance-tiers)|
| Sistema de arquivos | NFS|
| IOPS por gigabyte | 2|
| Intervalo de tamanho em gigabytes | 20-12.000 Gi|
| Disco rígido | SSD|
| Faturamento | Horário|
| Precificação | [Informações de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/file-storage/pricing)|
{: class="simple-tab-table"}
{: caption="Classe de armazenamento de arquivo: bronze" caption-side="top"}
{: #simpletabtable1}
{: tab-title="Bronze"}
{: tab-group="File storage class"}

| Características | Configuração|
|:-----------------|:-----------------|
| Nome | <code>ibmc-file-silver</code></br><code>ibmc-file-retain-silver</code>|
| Tipo | [Armazenamento do Endurance](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-endurance-tiers)|
| Sistema de arquivos | NFS|
| IOPS por gigabyte | 4|
| Intervalo de tamanho em gigabytes | 20-12.000 Gi|
| Disco rígido | SSD|
| Faturamento | Horário|
| Precificação | [Informações de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/file-storage/pricing)|
{: class="simple-tab-table"}
{: caption="Classe de armazenamento de arquivo: silver" caption-side="top"}
{: #simpletabtable2}
{: tab-title="Silver"}
{: tab-group="File storage class"}

| Características | Configuração|
|:-----------------|:-----------------|
| Nome | <code>ibmc-file-gold</code></br><code>ibmc-file-retain-gold</code>|
| Tipo | [Armazenamento do Endurance](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-endurance-tiers)|
| Sistema de arquivos | NFS|
| IOPS por gigabyte | 10|
| Intervalo de tamanho em gigabytes | 20 - 4.000 Gi|
| Disco rígido | SSD|
| Faturamento | Horário|
| Precificação | [Informações de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/file-storage/pricing)|
{: class="simple-tab-table"}
{: caption="Classe de armazenamento de arquivo: gold" caption-side="top"}
{: #simpletabtable3}
{: tab-title="Gold"}
{: tab-group="File storage class"}

| Características | Configuração|
|:-----------------|:-----------------|
| Nome | <code>ibmc-file-custom</code></br><code>ibmc-file-retain-custom</code>|
| Tipo | [Desempenho](/docs/infrastructure/FileStorage?topic=FileStorage-about#provisioning-with-performance)|
| Sistema de arquivos | NFS|
| IOPS e tamanho | <p><strong>Intervalo de tamanho em intervalo de gigabytes/IOPS em múltiplos de 100</strong></p><ul><li>20-39 Gi / 100-1000 IOPS</li><li>40-79 Gi / 100-2000 IOPS</li><li>80-99 Gi / 100-4000 IOPS</li><li>100-499 Gi / 100-6000 IOPS</li><li>500-999 Gi / 100-10000 IOPS</li><li>1000-1999 Gi / 100-20000 IOPS</li><li>2000-2999 Gi / 200-40000 IOPS</li><li>3000-3999 Gi / 200-48000 IOPS</li><li>4000-7999 Gi / 300-48000 IOPS</li><li>8000-9999 Gi / 500-48000 IOPS</li><li>10000-12000 Gi / 1000-48000 IOPS</li></ul>|
| Disco rígido | A razão de IOPS para gigabyte determina o tipo de disco rígido que é provisionado. Para determinar a sua razão de IOPS para gigabyte, você divide o IOPS pelo tamanho de seu armazenamento. </br></br>Exemplo: </br>Você escolheu 500 Gi de armazenamento com 100 IOPS. A sua razão é 0,2 (100 IOPS/500 Gi). </br></br><strong>Visão geral de tipos de disco rígido por razão:</strong><ul><li>Menor ou igual a 0,3: SATA</li><li>Maior que 0,3: SSD</li></ul>|
| Faturamento | Horário|
| Precificação | [Informações de precificação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/file-storage/pricing)|
{: class="simple-tab-table"}
{: caption="Classe de armazenamento de arquivo: customizado" caption-side="top"}
{: #simpletabtable4}
{: tab-title="Custom"}
{: tab-group="File storage class"}

<br />


## Classes de armazenamento customizado de amostra
{: #file_custom_storageclass}

É possível criar uma classe de armazenamento customizada e usar a classe de armazenamento no PVC.
{: shortdesc}

O {{site.data.keyword.containerlong_notm}} fornece [classes de armazenamento predefinidas](#file_storageclass_reference) para provisionar o armazenamento de arquivo com uma camada e uma configuração específicas. Em alguns casos, talvez você queira provisionar armazenamento com uma configuração diferente que não esteja coberta nas classes de armazenamento predefinidas. É possível usar os exemplos neste tópico para localizar classes de armazenamento customizadas de amostra.

Para criar sua classe de armazenamento customizada, consulte [Customizando uma classe de armazenamento](/docs/containers?topic=containers-kube_concepts#customized_storageclass). Em seguida, [use a sua classe de armazenamento customizada em seu PVC](#add_file).

### Criando armazenamento de reconhecimento de topologia
{: #file-topology}

Para usar o armazenamento de arquivo em um cluster com múltiplas zonas, seu pod deve ser planejado na mesma zona que sua instância de armazenamento de arquivo para que seja possível ler e gravar no volume. Antes da introdução do planejamento de volume com reconhecimento de topologia pelo Kubernetes, o fornecimento dinâmico de seu armazenamento criava automaticamente a instância de armazenamento de arquivo quando um PVC era criado. Em seguida, quando você criou seu pod, o planejador do Kubernetes tentou implementar o pod em um nó do trabalhador no mesmo data center que sua instância de armazenamento de arquivo.
{: shortdesc}

A criação da instância de armazenamento de arquivo sem conhecer as restrições do pod pode levar a resultados indesejados. Por exemplo, seu pod pode não estar apto a ser planejado para o mesmo nó do trabalhador que seu armazenamento porque o nó do trabalhador tem recursos insuficientes ou o nó do trabalhador está contaminado e não permite que o pod seja planejado. Com o planejamento de volume com reconhecimento de topologia, a instância de armazenamento de arquivo é atrasada até que o primeiro pod que usa o armazenamento seja criado.

O planejamento de volume com reconhecimento de topologia é suportado em clusters que executam somente o Kubernetes versão 1.12 ou mais recente.
{: note}

Os exemplos a seguir mostram como criar classes de armazenamento que atrasem a criação da instância de armazenamento de arquivo até que o primeiro pod que usa esse armazenamento esteja pronto para ser planejado. Para atrasar a criação, deve-se incluir a opção `volumeBindingMode: WaitForFirstConsumer`. Se você não incluir essa opção, o `volumeBindingMode` será configurado automaticamente como `Immediate` e a instância de armazenamento de arquivo será criada quando você criar o PVC.

- ** Exemplo para armazenamento de arquivo de Endurance: **
  ```
  apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: ibmc-file-bronze-delayed parameters: billingType: hourly classVersion: "2" iopsPerGB: "2" sizeRange: '[20-12000]Gi' type: Endurance provisioner: ibm.io/ibmc-file reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer
  ```
  {: codeblock}

- ** Exemplo para armazenamento de arquivo de desempenho: **
  ```
  apiVersion: storage.k8s.io/v1
  tipo: StorageClass
  metadados:
   nome: ibmc-file-performance-storageclass
   etiquetas:
     kubernetes.io/cluster-service: "true"
  Provisionador: ibm.io/ibmc-file
  parâmetros:
   billingType: "horária"
   classVersion: "2"
   sizeIOPSRange: |-
     "[ 20-39 ] Gi: [ 100-1000 ]"
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

### Especificando a zona para clusters de múltiplas zonas
{: #file_multizone_yaml}

Se você desejar criar seu armazenamento de arquivo em uma zona específica, será possível especificar a zona e a região em uma classe de armazenamento customizada.
{: shortdesc}

Use a classe de armazenamento customizada se você desejar [fornecer estaticamente o armazenamento de arquivo](#existing_file) em uma zona específica. Em todos os outros casos, [ especifique a zona diretamente em seu PVC](#add_file).
{: note}

Ao criar a classe de armazenamento customizada, especifique a mesma região e zona em que seus nós do cluster e do trabalhador estão. Para obter a região do seu cluster, execute `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>` e procure pelo prefixo da região na **URL principal**, como `eu-de` em `https://c2.eu-de.containers.cloud.ibm.com:11111`. Para obter a zona do seu nó do trabalhador, execute `ibmcloud oc workers --cluster <cluster_name_or_ID>`.

- ** Exemplo para armazenamento de arquivo de Endurance: **
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-file-silver-mycustom-storageclass
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-file
  parameters:
    zone: "dal12"
    region: "us-south"
    type: "Endurance"
    iopsPerGB: "4"
    sizeRange: "[20-12000]Gi"
    reclaimPolicy: "Delete"
    classVersion: "2"
  reclaimPolicy: Delete
  volumeBindingMode: Immediate
  ```
  {: codeblock}

- ** Exemplo para armazenamento de arquivo de desempenho: **
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
   name: ibmc-file-performance-storageclass
   labels:
     kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-file
  parameters:
   zone: "dal12"
   region: "us-south"
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
   type: "Performance"
  reclaimPolicy: Delete
  volumeBindingMode: Immediate
  ```
  {: codeblock}

### Mudando a versão do NFS padrão
{: #nfs_version_class}

A classe de armazenamento customizada a seguir permite que você defina a versão do NFS que você deseja fornecer. Por exemplo, para provisionar o NFS versão 3.0, substitua `<nfs_version>` por **3.0**.
{: shortdesc}

- ** Exemplo para armazenamento de arquivo de Endurance: **
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-file-mount
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-file
  parameters:
    type: "Endurance"
    iopsPerGB: "2"
    sizeRange: "[1-12000]Gi"
    reclaimPolicy: "Delete"
    classVersion: "2"
    mountOptions: nfsvers=<nfs_version>
  ```
  {: codeblock}

- ** Exemplo para armazenamento de arquivo de desempenho: **
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: ibmc-file-mount
    labels:
      kubernetes.io/cluster-service: "true"
  provisioner: ibm.io/ibmc-file
  parameters:
   type: "Performance"
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
   mountOptions: nfsvers=<nfs_version>
  ```
  {: codeblock}



