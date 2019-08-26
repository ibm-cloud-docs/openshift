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

# Entendendo as informações básicas de armazenamento do Kubernetes
{: #kube_concepts}

## Volumes persistentes e solicitações de volume persistente
{: #pvc_pv}

Antes de começar a provisionar o fornecimento, é importante entender os conceitos do Kubernetes de um volume persistente e de uma solicitação de volume persistente e como eles trabalham juntos em um cluster.
{: shortdesc}

A imagem a seguir mostra os componentes de armazenamento em um cluster.

<img src="images/cs_storage_pvc_pv.png" alt="Storage components in a cluster" width="275" style="width: 275px; border-style: none"/>

- **Cluster**</br> Por padrão, cada cluster é configurado com um plug-in para [provisionar o armazenamento de arquivo](/docs/containers?topic=containers-file_storage#add_file). É possível escolher instalar outros complementos, como aquele para [armazenamento de bloco](/docs/containers?topic=containers-block_storage). Para usar o armazenamento em um cluster, deve-se criar uma solicitação de volume persistente, um volume persistente e uma instância de armazenamento físico. Ao excluir o cluster, você tem a opção de excluir instâncias de armazenamento relacionadas.
- **Aplicativo**</br> Para ler e gravar na instância de armazenamento, deve-se montar a solicitação de volume persistente (PVC) para seu aplicativo. Os diferentes tipos de armazenamento têm regras de leitura/gravação diferentes. Por exemplo, é possível montar múltiplos pods para o mesmo PVC para armazenamento de arquivo. O armazenamento de bloco é fornecido com um modo de acesso RWO (ReadWriteOnce) de maneira que seja possível montar o armazenamento em somente um pod.
- **Solicitação de volume persistente (PVC)** </br> Uma PVC é a solicitação de provisionamento do armazenamento persistente com um tipo e uma configuração específicos. Para especificar o tipo de armazenamento persistente que você deseja, use as [Classes de armazenamento do Kubernetes](#storageclasses). O administrador de cluster pode definir classes de armazenamento ou é possível escolher dentre uma das classes de armazenamento predefinidas no {{site.data.keyword.containerlong_notm}}. Quando você cria um PVC, a solicitação é enviada para o provedor de armazenamento do {{site.data.keyword.Bluemix}}. Dependendo da configuração que está definida na classe de armazenamento, o dispositivo de armazenamento físico é solicitado e provisionado para sua conta de infraestrutura do IBM Cloud. Se a configuração solicitada não existir, o armazenamento não será criado.
- **Volume persistente (PV)** </br> Um PV é uma instância de armazenamento virtual incluída como um volume no cluster. O PV aponta para um dispositivo de armazenamento físico em sua conta de infraestrutura do IBM Cloud e resume a API que é usada para se comunicar com o dispositivo de armazenamento. Para montar um PV em um app, deve-se ter um PVC correspondente. Os PVs montados aparecem como uma pasta dentro do sistema de arquivos do contêiner.
- **Armazenamento físico** </br> Uma instância de armazenamento físico que pode ser usada para persistir seus dados. Exemplos de armazenamento físico no {{site.data.keyword.cloud_notm}} incluem [File Storage](/docs/containers?topic=containers-file_storage#file_storage), [Block Storage](/docs/containers?topic=containers-block_storage#block_storage), [Object Storage](/docs/containers?topic=containers-object_storage#object_storage) e armazenamento de nó do trabalhador local que podem ser usados como armazenamento SDS com o [Portworx](/docs/containers?topic=containers-portworx#portworx). O {{site.data.keyword.cloud_notm}} fornece alta disponibilidade para instâncias de armazenamento físico. No entanto, os dados que são armazenados em uma instância de armazenamento físico não são submetidos a backup automaticamente. Dependendo do tipo de armazenamento que você usa, existem métodos diferentes para configurar as soluções de backup e restauração.

Para obter mais informações sobre como criar e usar PVCs, PVs e o dispositivo de armazenamento físico, consulte:
- [ Provisionamento Dinâmico ](#dynamic_provisioning)
- [Provisionamento estático](#static_provisioning)

## Provisionamento dinâmico
{: #dynamic_provisioning}

Use o fornecimento dinâmico se você deseja fornecer aos desenvolvedores a liberdade de provisionar o armazenamento quando eles precisam.
{: shortdesc}

** Como ele funciona? **</br>

O fornecimento dinâmico é um recurso que é nativo para o Kubernetes e que permite que um desenvolvedor de cluster peça armazenamento com um tipo e configuração predefinidos sem saber todos os detalhes sobre como provisionar o dispositivo de armazenamento físico. Para abstrair os detalhes para o tipo de armazenamento específico, o administrador de cluster deve criar [classes de armazenamento](#storageclasses) que podem ser usadas pelo desenvolvedor ou usar as classes de armazenamento que são fornecidas com os plug-ins de armazenamento do {{site.data.keyword.Bluemix}}.

Para pedir o armazenamento, deve-se criar um PVC. O PVC determina a especificação para o armazenamento que você deseja provisionar. Após o PVC ser criado, o dispositivo de armazenamento e o PV serão criados automaticamente para você.  

A imagem a seguir mostra como o armazenamento de arquivo é provisionado dinamicamente em um cluster. Esse fluxo de amostra funciona semelhantemente a outros tipos de armazenamento, como o armazenamento de bloco.

**Fluxo de amostra para fornecimento dinâmico de armazenamento de arquivo com a classe de armazenamento prata predefinida**

<img src="images/cs_storage_dynamic.png" alt="Fluxo de amostra para provisionar armazenamento de arquivo dinamicamente em um cluster" width="500" style="width: 500px; border-style: none"/>

1. O usuário cria um persistent volume claim (PVC) que especifica o tipo de armazenamento, a classe de armazenamento, o tamanho em gigabytes, o número de IOPS e o tipo de faturamento. A classe de armazenamento determina o tipo de armazenamento que é provisionado e os intervalos permitidos para tamanho e IOPS. A criação de um PVC em um cluster aciona automaticamente o plug-in de armazenamento para o tipo solicitado de armazenamento para provisionar armazenamento com a especificação fornecida.
2. O dispositivo de armazenamento é automaticamente solicitado e provisionado para sua conta de infraestrutura do IBM Cloud. O ciclo de faturamento para seu dispositivo de armazenamento é iniciado.
3. O plug-in de armazenamento cria automaticamente um volume persistente (PV) no cluster, um dispositivo de armazenamento virtual que aponta para o dispositivo de armazenamento real em sua conta de infraestrutura do IBM Cloud.
4. O PVC e o PV são conectados automaticamente um ao outro. O status do PVC e do PV muda para `Bound`. Agora é possível usar o PVC para montar armazenamento persistente em seu app. Se você excluir a PVC, o PV e a instância de armazenamento relacionada também serão excluídos. </br>

** Quando uso o fornecimento dinâmico? **</br>

Revise os casos de uso comuns a seguir para fornecimento dinâmico:
1. **Provisionar armazenamento quando necessário:** em vez de pré-fornecer armazenamento persistente para desenvolvedores e pagar por armazenamento não usado, é possível fornecer aos desenvolvedores a liberdade de provisionar o armazenamento quando eles precisam. Para determinar o tipo de armazenamento que o desenvolvedor pode provisionar, é possível definir [classes de armazenamento](#storageclasses).
2. **Automatizar a criação de PVC, PV e dispositivo de armazenamento:** você deseja provisionar e desprover automaticamente o armazenamento sem intervenção manual de um administrador de cluster.
3. **Criar e excluir armazenamento frequentemente:** você tem um app ou configurou um pipeline de entrega contínua que cria e remove o armazenamento persistente regularmente. O armazenamento persistente que é provisionado dinamicamente com uma classe de armazenamento sem retenção pode ser removido excluindo o PVC.

Para obter mais informações sobre como provisionar dinamicamente o armazenamento persistente, consulte:
- [Armazenamento de arquivo](/docs/containers?topic=containers-file_storage#add_file)
- [ Bloquear armazenamento ](/docs/containers?topic=containers-block_storage#add_block)

## Provisionamento estático
{: #static_provisioning}

Se você tiver um dispositivo de armazenamento persistente existente em sua conta de infraestrutura do IBM Cloud, será possível usar o provisionamento estático para tornar a instância de armazenamento disponível para seu cluster.
{: shortdesc}

** Como ele funciona? **</br>

O fornecimento estático é um recurso nativo para o Kubernetes que permite que os administradores de cluster disponibilizem dispositivos de armazenamento existentes para um cluster. Como um administrador de cluster, deve-se saber os detalhes do dispositivo de armazenamento, suas configurações suportadas e as opções de montagem.  

Para tornar o armazenamento existente disponível para um usuário do cluster, é necessário criar manualmente o dispositivo de armazenamento, um PV e um PVC.  

A imagem a seguir mostra como provisionar estaticamente o armazenamento de arquivo em um cluster. Este fluxo de amostra funciona de forma semelhante a outros tipos de armazenamento, como armazenamento de bloco.

**Fluxo de amostra para fornecimento estático de armazenamento de arquivo**

<img src="images/cs_storage_static.png" alt="Fluxo de amostra para provisionar estaticamente o armazenamento de arquivo em um cluster" width="500" style="width: 500px; border-style: none"/>

1. O administrador de cluster reúne todos os detalhes sobre o dispositivo de armazenamento existente e cria um volume persistente (PV) no cluster.
2. Com base nos detalhes de armazenamento no PV, o plug-in de armazenamento conecta-se ao PV com o dispositivo de armazenamento em sua conta de infraestrutura do IBM Cloud.
3. O administrador de cluster ou um desenvolvedor cria um PVC. Como o PV e o dispositivo de armazenamento já existem, nenhuma classe de armazenamento é especificada no PVC.
4. Depois que o PVC é criado, o plug-in de armazenamento tenta corresponder o PVC a um PV existente. O PVC e o PV correspondem quando os mesmos valores para o tamanho, IOPS e modo de acesso são usados no PVC e no PV. Quando o PVC e o PV correspondem, o status do PVC e do PV muda para `Bound`. Agora é possível usar o PVC para montar armazenamento persistente em seu app. Quando você exclui o PVC, o PV e a instância de armazenamento físico não são removidos. Deve-se remover a PVC, o PV e a instância de armazenamento físico separadamente.  </br>

** Quando eu utilizo fornecimento estático? **</br>

Revise os casos de uso comuns a seguir para fornecimento estático de armazenamento persistente:
1. **Tornar os dados retidos disponíveis para o cluster:** você provisionou o armazenamento persistente com uma classe de armazenamento de retenção usando fornecimento dinâmico. Você removeu o PVC, mas o PV, o armazenamento físico na infraestrutura do IBM Cloud, e os dados ainda existem. Você deseja acessar os dados retidos por meio de um app em seu cluster.
2. **Use um dispositivo de armazenamento existente:** você provisionou o armazenamento persistente diretamente em sua conta de infraestrutura do IBM Cloud e deseja usar esse dispositivo de armazenamento em seu cluster.
3. **Compartilhar armazenamento persistente entre clusters na mesma zona:** você provisionou o armazenamento persistente para seu cluster. Para compartilhar a mesma instância de armazenamento persistente com outros clusters na mesma zona, deve-se criar manualmente o PV e o PVC correspondente no outro cluster. **Nota:** o compartilhamento de armazenamento persistente em clusters estará disponível somente se o cluster e a instância de armazenamento estiverem localizados na mesma zona.
4. **Compartilhar armazenamento persistente entre namespaces no mesmo cluster:** você provisionou o armazenamento persistente em um namespace de seu cluster. Você deseja usar a mesma instância de armazenamento para um pod de app que é implementado em um namespace diferente em seu cluster.

Para obter mais informações sobre como provisionar armazenamento estaticamente, consulte:
- [Armazenamento de arquivo](/docs/containers?topic=containers-file_storage#file_predefined_storageclass)
- [ Bloquear armazenamento ](/docs/containers?topic=containers-block_storage#block_predefined_storageclass)

## Classes de armazenamento
{: #storageclasses}

Para provisionar dinamicamente o armazenamento persistente, deve-se definir o tipo e a configuração do armazenamento que você deseja.
{: shortdesc}

Uma [classe de armazenamento do Kubernetes ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/storage/storage-classes/) é usada para abstrair a plataforma de armazenamento subjacente que é suportada em {{site.data.keyword.cloud_notm}} para que você não tenha que saber todos os detalhes sobre tamanhos suportados, IOPS ou políticas de retenção para provisionar com êxito o armazenamento persistente em um cluster. O {{site.data.keyword.containerlong_notm}} fornece classes de armazenamento predefinidas para cada tipo de armazenamento que é suportado. Cada classe de armazenamento é projetada para abstrair a camada de armazenamento suportada enquanto lhe dá a opção de decidir sobre o tamanho, o IOPS e a política de retenção que você deseja.

Para obter as especificações de classe de armazenamento predefinidas, consulte:
- [Armazenamento de arquivo](/docs/containers?topic=containers-file_storage#file_storageclass_reference)
- [ Bloquear armazenamento ](/docs/containers?topic=containers-block_storage#block_storageclass_reference)

Não está localizando o que você procura? Também é possível criar sua própria classe de armazenamento customizada para provisionar o tipo de armazenamento desejado.
{: tip}

### Customizando uma classe de armazenamento
{: #customized_storageclass}

Se não for possível usar uma das classes de armazenamento fornecidas, será possível criar sua própria classe de armazenamento customizada. Você pode desejar customizar uma classe de armazenamento para especificar configurações como a zona, o tipo de sistema de arquivos, o tipo de servidor ou as opções de modo de ligação de volume do [ ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode) (somente armazenamento de bloco).
{: shortdesc}

1. Crie uma classe de armazenamento customizada. É possível iniciar usando uma das classes de armazenamento predefinidas ou efetuar check-out de nossas classes de armazenamento customizadas de amostra.
   - Classes de armazenamento predefinidas:
     - [Armazenamento de arquivo](/docs/containers?topic=containers-file_storage#file_storageclass_reference)
     - [ Bloquear armazenamento ](/docs/containers?topic=containers-block_storage#block_storageclass_reference)
   - Classes de armazenamento customizado de amostra:
     - [Armazenamento de arquivo](/docs/containers?topic=containers-file_storage#file_custom_storageclass)
     - [ Bloquear armazenamento ](/docs/containers?topic=containers-block_storage#block_custom_storageclass)

2. Crie a classe de armazenamento customizada.
   ```
   oc apply -f <local_file_path>
   ```
   {: pre}

3.  Verifique se a classe de armazenamento customizada foi criada.
    ```
    oc get storageclasses                                                        
    ```
    {: pre}

4. Crie um persistent volume claim (PVC) para provisionar dinamicamente o armazenamento com sua classe de armazenamento customizada.
   - [Armazenamento de arquivo](/docs/containers?topic=containers-file_storage#add_file)
   - [ Bloquear armazenamento ](/docs/containers?topic=containers-block_storage#add_block)

5. Verifique se o PVC foi criado e ligado a um volume persistente (PV). Esse processo pode levar alguns minutos para ser concluído.
   ```
   oc get pvc
   ```
   {: pre}

### Mudando ou atualizando para uma classe de armazenamento diferente
{: #update_storageclass}

Quando você provisiona dinamicamente o armazenamento persistente usando uma classe de armazenamento, você provisiona o armazenamento persistente com uma configuração específica. Não é possível mudar o nome da classe de armazenamento ou o tipo de armazenamento provisionado. No entanto, você tem a opção de escalar seu armazenamento conforme mostrado na tabela a seguir.
{: shortdesc}

<table>
<caption>Visão geral de opções de ajuste de escala para soluções de armazenamento do {{site.data.keyword.containerlong_notm}}</caption>
<thead>
<th>Solução de armazenamento</th>
<th>Opções de ajuste de escala</th>
</thead>
<tbody>
<tr>
<td>Armazenamento de arquivo</td>
<td>É possível aumentar o tamanho de armazenamento e IOPS designados [modificando seu volume existente](/docs/containers?topic=containers-file_storage#file_change_storage_configuration). </td>
</tr>
<tr>
<td>Armazenamento de bloco</td>
<td>É possível aumentar o tamanho de armazenamento e IOPS designados [modificando seu volume existente](/docs/containers?topic=containers-block_storage#block_change_storage_configuration). </td>
</tr>
<tr>
<td>Armazenamento de objetos</td>
<td>Seu volume é escalado automaticamente em tamanho e você é cobrado com base em seu consumo real. No entanto, não é possível mudar os atributos de desempenho de seu volume à medida que eles são definidos na classe de armazenamento usada para criar seu depósito no {{site.data.keyword.cos_full_notm}}. Para mudar para uma classe de armazenamento diferente, deve-se provisionar um novo depósito usando a classe de armazenamento que você deseja. Em seguida, copie seus dados do depósito antigo para o novo. </td>
</tr>
</tbody>
</table>


## Preparando o armazenamento existente para uso de múltiplas zonas com rótulos do Kubernetes
{: #storage_multizone}

Se você atualizou seu cluster de uma zona única para um cluster de múltiplas zonas e tinha persistent volumes (PVs) existentes, inclua os rótulos de zona e região do Kubernetes em seus PVs. Os rótulos asseguram que os pods que montam esse armazenamento sejam implementados na zona em que o armazenamento persistente existe.
{:shortdesc}

Essas etapas serão necessárias somente se você tiver PVs existentes que foram criados antes que os recursos de várias zonas estivessem disponíveis. Os PVs que foram criados depois que as múltiplas zonas ficaram disponíveis já incluem os rótulos de região e zona do Kubernetes.
{: note}

Use um script para localizar todos os PVs em seu cluster e aplique os rótulos do Kubernetes `failure-domain.beta.kubernetes.io/region` e `failure-domain.beta.beta.kubernetes.io/zone`. Se o PV já tiver os rótulos, o script não sobrescreverá os valores existentes.

Antes de iniciar:
- [Destine a CLI do Kubernetes para o cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).
- Se você tiver múltiplas VLANs para um cluster, múltiplas sub-redes na mesma VLAN ou em um cluster multizona, você deverá ativar um [Virtual Router Function (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) para sua conta de infraestrutura do IBM Cloud para que os nós do trabalhador possam se comunicar entre si na rede privada. Para ativar o VRF, [entre em contato com o seu representante de conta de infraestrutura do IBM Cloud](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Para verificar se um VRF já está ativado, use o comando `ibmcloud account show`. Se não for possível ou você não desejar ativar o VRF, ative o [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Para executar essa ação, você precisa da [permissão de infraestrutura](/docs/containers?topic=containers-users#infra_access) **Rede > Gerenciar a rede VLAN Spanning** ou é possível solicitar ao proprietário da conta para ativá-la. Para verificar se a ampliação da VLAN já está ativada, use o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud oc vlan-spanning-get --region <region>`.

Para atualizar PVs existentes:

1.  Aplique os rótulos de múltiplas zonas a seus PVs executando o script.  Substitua <mycluster> pelo nome de seu cluster. Quando solicitado, confirme a atualização de seus PVs.

    ```
    bash <(curl -Ls https://raw.githubusercontent.com/IBM-Cloud/kube-samples/master/file-pv-labels/apply_pv_labels.sh) <mycluster>
    ```
    {: pre}

    **Saída de exemplo**:

    ```
    Retrieving cluster storage...
    OK

    Name:			mycluster
    ID:			  myclusterID1234
    State:			normal
    ...
    Addons
    Name                   Enabled
    storage-watcher-pod    true
    basic-ingress-v2       true
    customer-storage-pod   true
    us-south
    kube-config-dal10-storage.yml
    storage.yml
    dal10\n
    The persistent volumes which do not have region and zone labels will be updated with REGION=
    us-south and ZONE=dal10. Are you sure to continue (y/n)?y
    persistentvolume "pvc-ID-123456" labeled
    persistentvolume "pvc-ID-789101" labeled
    ['failure-domain.beta.kubernetes.io/region' already has a value (us-south), and --overwrite is false, 'failure-domain.beta.kubernetes.io/zone' already has a value (dal10), and --overwrite is false]
    ['failure-domain.beta.kubernetes.io/region' already has a value (us-south), and --overwrite is false, 'failure-domain.beta.kubernetes.io/zone' already has a value (dal10), and --overwrite is false]
    \nSuccessfully applied labels to persistent volumes which did not have region and zone labels.
    ```
    {: screen}

2.  Verifique se os rótulos foram aplicados a seus PVs.

    1.  Consulte a saída do comando anterior para os IDs de PVs que foram rotulados.

        ```
        persistentvolume "pvc-ID-123456" labeled
        persistentvolume "pvc-ID-789101" labeled
        ```
        {: screen}

    2.  Revise os rótulos de região e zona para seus PVs.

        ```
        oc describe pv pvc-ID-123456
        ```
        {: pre}

        **Saída de exemplo**:
        ```
        Name:		pvc-ID-123456
        Labels:		CapacityGb=4
        		Datacenter=dal10
            ...
        		failure-domain.beta.kubernetes.io/region=us-south
        		failure-domain.beta.kubernetes.io/zone=dal10
            ...
        ```
        {: screen}

**O que vem a seguir?**

Agora que você rotulou seus PVs existentes, é possível montar o PV em seu cluster de múltiplas zonas. Consulte os links a seguir para obter mais informações.
- Use  [ armazenamento de arquivo NFS existente ](/docs/containers?topic=containers-file_storage#existing_file)
- Use  [ armazenamento de bloco existente ](/docs/containers?topic=containers-block_storage#existing_block)


