---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: openshift, rhoks, roks, rhos, multi az, multi-az, szr, mzr

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


# Planejando a configuração de rede de cluster
{: #plan_clusters}

Projete uma configuração de rede para seus clusters do {{site.data.keyword.openshiftlong}} que atenda às necessidades de suas cargas de trabalho e ambiente.
{: shortdesc}

Os seus aplicativos conteinerizados são hospedados em hosts de cálculo que são chamados de nós do trabalhador. Os nós do trabalhador são gerenciados pelo mestre. A configuração da comunicação entre nós do trabalhador e o mestre, outros serviços, a Internet ou outras redes privadas depende de como você configura sua rede de infraestrutura do IBM Cloud.

Primeira criação de um cluster? Primeiro, teste o [tutorial Criando clusters do OpenShift](/docs/openshift?topic=openshift-openshift_tutorial). Em seguida, volte aqui quando estiver pronto para planejar seus clusters prontos para produção.
{: tip}

Para planejar sua configuração de rede de cluster, primeiro [entenda os fundamentos de rede de cluster](#plan_basics). Em seguida, é possível revisar três potenciais configurações de rede de cluster que são adequadas para cenários baseados em ambiente, incluindo [executar cargas de trabalho do app voltadas para a Internet](#internet-facing), [ampliar um data center no local com acesso público limitado](#limited-public) e [ampliar um data center no local somente de rede privada](#private_clusters).

## Entendendo os fundamentos de rede de cluster
{: #plan_basics}

Ao criar seu cluster, deve-se escolher uma configuração de rede para que determinados componentes do cluster possam se comunicar entre si e com redes ou serviços fora do cluster.
{: shortdesc}

* [Comunicação de trabalhador para trabalhador](#worker-worker): todos os nós do trabalhador devem ser capazes de se comunicar entre si na rede privada. Em muitos casos, a comunicação deve ser permitida em múltiplas VLANs privadas para permitir que trabalhadores em VLANs diferentes e em zonas diferentes se conectem entre si.
* [Comunicação de trabalhador para principal e de usuário para principal](#workeruser-master): seus nós do trabalhador e seus usuários do cluster autorizados podem se comunicar com o principal do Kubernetes de forma segura pela rede pública com TLS ou pela rede privada por meio de terminais em serviço privado.
* [Comunicação do trabalhador para outros serviços do {{site.data.keyword.cloud_notm}} ou redes no local](#worker-services-onprem): permita que os nós do trabalhador se comuniquem de forma segura com outros serviços do {{site.data.keyword.cloud_notm}}, como {{site.data.keyword.registrylong}} e com uma rede no local.
* [Comunicação externa para apps que são executados em nós do trabalhador](#external-workers): permita solicitações públicas ou privadas no cluster, bem como solicitações fora do cluster em um terminal público.

### Comunicação de trabalhador para trabalhador
{: #worker-worker}

Quando você cria um cluster, os nós do trabalhador do cluster são conectados automaticamente a uma VLAN privada e, opcionalmente, conectados a uma VLAN pública. Uma VLAN configura um grupo de nós do trabalhador e pods como se eles estivessem conectados à mesma ligação física e fornece um canal para conectividade entre os trabalhadores.
{: shortdesc}

**Conexões de VLAN para nós do trabalhador**</br>
Todos os nós do trabalhador devem ser conectados a uma VLAN privada para que cada nó do trabalhador possa enviar e receber informações para outros nós do trabalhador. Ao criar um cluster com nós do trabalhador que também estão conectados a uma VLAN pública, os nós do trabalhador poderão se comunicar com o principal do Kubernetes automaticamente pela VLAN pública e pela VLAN privada, se você ativar o terminal em serviço privado. A VLAN pública também fornece conectividade de rede pública para que seja possível expor apps em seu cluster na Internet. No entanto, se você precisar proteger seus apps na interface pública, várias opções estarão disponíveis para proteger seu cluster, como usar políticas de rede do Calico ou isolar a carga de trabalho de rede externa para os nós do trabalhador de borda.
* Clusters grátis: em clusters grátis, os nós do trabalhador do cluster são conectados a uma VLAN pública e VLAN privada de propriedade da IBM por padrão. Como a IBM controla as VLANs, as sub-redes e os endereços IP, não é possível criar clusters de múltiplas zonas ou incluir sub-redes em seu cluster e é possível usar somente serviços NodePort para expor seu app.</dd>
* Clusters padrão: em clusters padrão, a primeira vez que você cria um cluster em uma zona, uma VLAN pública e uma VLAN privada nessa zona são automaticamente provisionadas para você em sua conta de infraestrutura do IBM Cloud. Se você especificar que os nós do trabalhador devem ser conectados a somente uma VLAN privada, somente uma VLAN privada nessa zona será provisionada automaticamente. Para cada cluster subsequente que for criado nessa zona, será possível especificar o par de VLANs que você deseja usar. É possível reutilizar as mesmas VLANs públicas e privadas que foram criadas para você porque múltiplos clusters podem compartilhar VLANs.

Para obter mais informações sobre VLANs, sub-redes e endereços IP, consulte [Visão geral de rede no {{site.data.keyword.containerlong_notm}}](/docs/containers?topic=containers-subnets#basics).

**Comunicação de nó do trabalhador entre sub-redes e VLANs**</br>
Em várias situações, os componentes em seu cluster devem ter permissão para se comunicar entre múltiplas VLANs privadas. Por exemplo, se você desejar criar um cluster de múltiplas zonas, se você tiver múltiplas VLANs para um cluster ou se tiver múltiplas sub-redes na mesma VLAN, os nós do trabalhador em sub-redes diferentes na mesma VLAN ou em VLANs diferentes não poderão se comunicar automaticamente entre si. Deve-se ativar o Virtual Routing and Forwarding (VRF) ou a ampliação de VLAN para sua conta de infraestrutura do IBM Cloud.

* [Virtual Routing and Forwarding (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud): o VRF permite que todas as VLANs privadas e sub-redes em sua conta de infraestrutura se comuniquem entre si. Além disso, o VRF é necessário para permitir que seus trabalhadores e o principal se comuniquem pelo terminal em serviço privado e se comuniquem com outras instâncias do {{site.data.keyword.cloud_notm}} que suportam terminais em serviço privado. Para verificar se um VRF já está ativado, use o comando `ibmcloud account show`. Para ativar o VRF, execute `ibmcloud account update --service-endpoint-enable true`. Essa saída de comando solicita que você abra um caso de suporte para ativar sua conta para usar o VRF e os terminais em serviço. O VRF elimina a opção VLAN Spanning para sua conta porque todas as VLANs são capazes de se comunicar.</br></br>
Quando o VRF for ativado, qualquer sistema que estiver conectado a qualquer uma das VLANs privadas na mesma conta do {{site.data.keyword.cloud_notm}} poderá se comunicar com os nós do trabalhador do cluster. É possível isolar seu cluster de outros sistemas na rede privada, aplicando [políticas de rede privada do Calico](/docs/containers?topic=containers-network_policies#isolate_workers).</dd>
* [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning): se você não puder ou não desejar ativar o VRF, por exemplo, se não precisar que o principal seja acessível na rede privada ou se usar um dispositivo de gateway para acessar o principal pela VLAN pública, ative o VLAN Spanning. Por exemplo, se você tiver um dispositivo de gateway existente e, em seguida, incluir um cluster, as novas sub-redes móveis que forem pedidas para o cluster não serão configuradas no dispositivo de gateway, mas o VLAN Spanning ativará o roteamento entre as sub-redes. Para ativar o VLAN Spanning, você precisa da [permissão de infraestrutura](/docs/containers?topic=containers-users#infra_access) **Rede > Gerenciar VLAN Spanning de rede** ou é possível solicitar ao proprietário da conta para ativá-lo. Para verificar se a ampliação de VLAN já está ativada, use o [comando](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud oc vlan-spanning-get`. Não será possível ativar o terminal em serviço privado se você escolher ativar o VLAN Spanning em vez do VRF.

</br>

### Comunicação de trabalhador para principal e de usuário para principal
{: #workeruser-master}

Um canal de comunicação deve ser configurado para que os nós do trabalhador possam estabelecer uma conexão com o principal do Kubernetes. É possível permitir que seus nós do trabalhador e o principal do Kubernetes se comuniquem ativando somente o terminal em serviço público, os terminais em serviço público e privado ou somente o terminal em serviço privado.
{: shortdesc}

Para proteger a comunicação por terminais em serviço público e privado, o {{site.data.keyword.containerlong_notm}} configura automaticamente uma conexão OpenVPN entre o principal do Kubernetes e o nó do trabalhador quando o cluster é criado. Os trabalhadores conversam de forma segura com o principal por meio de certificados TLS e o principal conversa com os trabalhadores por meio da conexão OpenVPN.

**Somente terminal em serviço público**</br>
Se você não desejar ou não puder ativar o VRF para sua conta, seus nós do trabalhador poderão se conectar automaticamente ao principal do Kubernetes pela VLAN pública por meio do terminal em serviço público.
* A comunicação entre os nós do trabalhador e o principal é estabelecida de forma segura pela rede pública por meio do terminal em serviço público.
* O principal é publicamente acessível aos usuários do cluster autorizados somente por meio do terminal em serviço público. Os usuários do cluster podem acessar seu mestre do Kubernetes com segurança pela Internet para executar comandos `oc`, por exemplo.

**Terminais em serviço público e privado**</br>
Para tornar seu principal acessível de forma pública ou privada aos usuários do cluster, é possível ativar os terminais em serviço público e privado. O VRF é necessário em sua conta do {{site.data.keyword.cloud_notm}} e deve-se ativar sua conta para usar os terminais em serviço. Para ativar o VRF e os terminais em serviço, execute `ibmcloud account update --service-endpoint-enable true`.
* Se os nós do trabalhador estiverem conectados a VLANs públicas e privadas, a comunicação entre os nós do trabalhador e o principal será estabelecida pela rede privada por meio do terminal em serviço privado e pela rede pública por meio do terminal em serviço público. Ao rotear metade do tráfego do trabalhador para o principal pelo terminal público e metade pelo terminal privado, a comunicação entre eles é protegida contra possíveis indisponibilidades da rede pública ou da rede privada. Se os nós do trabalhador estiverem conectados a somente VLANs privadas, a comunicação entre os nós do trabalhador e o principal será estabelecida pela rede privada somente por meio do terminal em serviço privado.
* O mestre é publicamente acessível aos usuários de cluster autorizados por meio do terminal em serviço público. O principal é acessível de forma privada por meio do terminal em serviço privado se os usuários do cluster autorizados estão em sua rede privada do {{site.data.keyword.cloud_notm}} ou estão conectados à rede privada por meio de uma conexão VPN ou do {{site.data.keyword.cloud_notm}} Direct Link. Observe que se deve [expor o terminal principal por meio de um balanceador de carga privado](/docs/containers?topic=containers-clusters#access_on_prem) para que os usuários possam acessar o principal por meio de uma conexão VPN ou {{site.data.keyword.cloud_notm}} Direct Link.

**Somente terminal em serviço privado**</br>
Para tornar seu principal acessível somente de forma privada, é possível ativar o terminal em serviço privado. O VRF é necessário em sua conta do {{site.data.keyword.cloud_notm}} e deve-se ativar sua conta para usar os terminais em serviço. Para ativar o VRF e os terminais em serviço, execute `ibmcloud account update --service-endpoint-enable true`. Observe que o uso somente do terminal em serviço privado não incorre em encargos de largura da banda faturados ou medidos.
* A comunicação entre os nós do trabalhador e o principal é estabelecida pela rede privada por meio do terminal em serviço privado.
* O principal será acessível de forma privada se os usuários do cluster autorizados estiverem em sua rede privada do {{site.data.keyword.cloud_notm}} ou estiverem conectados à rede privada por meio de uma conexão VPN ou DirectLink. Observe que se deve [expor o terminal principal por meio de um balanceador de carga privado](/docs/containers?topic=containers-clusters#access_on_prem) para que os usuários possam acessar o principal por meio de uma conexão VPN ou DirectLink.

</br>

### Comunicação do trabalhador com outros serviços do {{site.data.keyword.cloud_notm}} ou redes no local
{: #worker-services-onprem}

Permita que os nós do trabalhador se comuniquem de forma segura com outros serviços do {{site.data.keyword.cloud_notm}}, como o {{site.data.keyword.registrylong}}, e com uma rede no local.
{: shortdesc}

**Comunicação com outros serviços do {{site.data.keyword.cloud_notm}} por meio da rede privada ou pública**</br> Os nós do trabalhador podem se comunicar automaticamente com outros serviços do {{site.data.keyword.cloud_notm}} que suportam terminais em serviço privados, como o {{site.data.keyword.registrylong}}, por meio da rede privada de infraestrutura do IBM Cloud. Se um serviço do {{site.data.keyword.cloud_notm}} não suportar terminais em serviço privado, os nós do trabalhador deverão ser conectados a uma VLAN pública para que eles possam se comunicar de forma segura com os serviços pela rede pública.

Se você usar políticas do Calico ou um dispositivo de gateway para controlar as redes públicas ou privadas de seus nós do trabalhador, deverá permitir o acesso aos endereços IP públicos dos serviços que suportam terminais em serviço público e, opcionalmente, aos endereços IP privados dos serviços que suportam terminais em serviço privados.
* [Permitir acesso aos endereços IP públicos dos serviços nas políticas do Calico](/docs/containers?topic=containers-network_policies#isolate_workers_public)
* [Permitir acesso aos endereços IP privados de serviços que suportam terminais em serviço privado nas políticas do Calico](/docs/containers?topic=containers-network_policies#isolate_workers)
* [Permitir acesso aos endereços IP públicos de serviços e aos endereços IP privados de serviços que suportam terminais em serviço privados em um firewall de dispositivo de gateway](/docs/containers?topic=containers-firewall#firewall_outbound)

**{{site.data.keyword.BluDirectLink}} para comunicação pela rede privada com recursos em data centers no local**</br>
Para conectar seu cluster ao seu data center no local, como com o {{site.data.keyword.icpfull_notm}}, é possível configurar o [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link). Com o {{site.data.keyword.cloud_notm}} Direct Link, você cria uma conexão direta e privada entre seus ambientes de rede remota e o {{site.data.keyword.containerlong_notm}} sem rotear pela Internet pública.

**Conexão VPN IPSec do strongSwan para comunicação pela rede pública com recursos em data centers no local**
* Nós do trabalhador que estão conectados a VLANs públicas e privadas: configure um [serviço VPN IPSec do strongSwan ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.strongswan.org/about.html) diretamente em seu cluster. O serviço de VPN do IPSec do strongSwan fornece um canal de comunicação seguro de ponta a ponta sobre a Internet que é baseado no conjunto de protocolos padrão de mercado da Internet Protocol Security (IPSec). Para configurar uma conexão segura entre seu cluster e uma rede no local, [configure e implemente o serviço VPN IPSec do strongSwan](/docs/containers?topic=containers-vpn#vpn-setup) diretamente em um pod no cluster.
* Nós do trabalhador conectados a somente uma VLAN privada: configure um terminal VPN IPSec em um dispositivo de gateway, como um Virtual Router Appliance (Vyatta). Em seguida, [configure o serviço VPN IPSec do strongSwan](/docs/containers?topic=containers-vpn#vpn-setup) em seu cluster para usar o terminal VPN em seu gateway. Se você não desejar usar o strongSwan, será possível [configurar a conectividade VPN diretamente com o VRA](/docs/containers?topic=containers-vpn#vyatta).

</br>

### Comunicação externa para apps que são executados em nós do trabalhador
{: #external-workers}

Permita solicitações de tráfego público ou privado de fora do cluster para seus apps que são executados em nós do trabalhador.
{: shortdesc}

**Tráfego privado para apps de cluster**</br>
Ao implementar um app em seu cluster, você talvez deseje tornar o aplicativo acessível somente para usuários e serviços que estão na mesma rede privada que o seu cluster. O balanceamento de carga privado é ideal para tornar seu aplicativo disponível para solicitações de fora do cluster sem o expor ao público em geral. Também é possível usar o balanceamento de carga privado para testar o acesso, o roteamento de solicitação e outras configurações para seu aplicativo antes de ele ser exposto posteriormente para o público com serviços de rede pública. Para permitir solicitações de tráfego privado de fora do cluster para seus apps, é possível criar serviços de rede privada do Kubernetes, como NodePorts privados, NLBs e ALBs do Ingress. Em seguida, é possível usar as políticas pré-DNAT do Calico para bloquear o tráfego para NodePorts públicos de serviços de rede privada. Para obter mais informações, consulte [Planejando o balanceamento de carga externa privada](/docs/containers?topic=containers-cs_network_planning#private_access).

**Tráfego público para apps de cluster**</br>
Para tornar seus apps externamente acessíveis por meio da Internet pública, é possível criar NodePorts públicos, balanceadores de carga de rede (NLBs) e balanceadores de carga do aplicativo (ALBs) do Ingress. Os serviços de rede pública se conectam a essa interface de rede pública, fornecendo a seu app um endereço IP público e, opcionalmente, uma URL pública. Quando um aplicativo é publicamente exposto, qualquer pessoa que tenha o endereço IP de serviço público ou a URL configurada para ele pode enviar uma solicitação para seu aplicativo. Em seguida, é possível usar as políticas pré-DNAT do Calico para controlar o tráfego para serviços de rede pública, como incluir na lista de desbloqueio o tráfego de somente determinados endereços IP de origem ou CIDRs e bloquear todo o outro tráfego. Para obter mais informações, consulte [Planejando o balanceamento de carga externa pública](/docs/containers?topic=containers-cs_network_planning#private_access).

Para obter segurança adicional, isole as cargas de trabalho de rede para os nós do trabalhador de borda. Os nós do trabalhador de borda podem melhorar a segurança de seu cluster permitindo que menos nós do trabalhador conectados a VLANs públicas sejam acessados externamente e isolando a carga de trabalho de rede. Quando você [rotula nós do trabalhador como nós de borda](/docs/containers?topic=containers-edge#edge_nodes), os pods NLB e ALB são implementados somente para os nós do trabalhador especificados. Para evitar também que outras cargas de trabalho sejam executadas em nós de borda, é possível [contaminar os nós de borda](/docs/containers?topic=containers-edge#edge_workloads). No Kubernetes versão 1.14 e mais recente, é possível implementar NLBs e ALBs públicos e privados em nós de borda.
Por exemplo, se os nós do trabalhador estiverem conectados a somente uma VLAN privada, mas você precisar permitir acesso público a um app em seu cluster, será possível criar um conjunto de trabalhadores de borda no qual os nós de borda estão conectados a VLANs públicas e privadas. É possível implementar NLBs e ALBs públicos nesses nós de borda para assegurar que somente esses trabalhadores manipulem conexões públicas.

Se os nós do trabalhador estiverem conectados a somente uma VLAN privada e você usar um dispositivo de gateway para fornecer comunicação entre os nós do trabalhador e o cluster principal, também será possível configurar o dispositivo como um firewall público ou privado. Para permitir solicitações de tráfego público ou privado de fora do cluster para seus apps, é possível criar NodePorts públicos ou privados, NLBs e ALBs do Ingress. Em seguida, deve-se [abrir as portas necessárias e os endereços IP](/docs/containers?topic=containers-firewall#firewall_inbound) em seu firewall de dispositivo de gateway para permitir o tráfego de entrada para esses serviços pela rede pública ou privada.
{: note}

<br />


## Cenário: executar cargas de trabalho do app voltadas para a Internet em um cluster
{: #internet-facing}

Neste cenário, você deseja executar cargas de trabalho em um cluster que são acessíveis a solicitações da Internet para que os usuários finais possam acessar seus apps. Você deseja a opção de isolar o acesso público em seu cluster e de controlar quais solicitações públicas são permitidas para seu cluster. Além disso, seus trabalhadores têm acesso automático a quaisquer serviços do {{site.data.keyword.cloud_notm}} que você deseja conectar com seu cluster.
{: shortdesc}

<p>
<figure>
 <img src="images/cs_clusters_planning_internet.png" alt="Imagem de arquitetura para um cluster que executa cargas de trabalho voltadas para a Internet"/>
 <figcaption> Arquitetura para um cluster que executa cargas de trabalho voltadas para a Internet </figcaption>
</figure>
</p>

Para alcançar essa configuração, você cria um cluster conectando os nós do trabalhador a VLANs públicas e privadas.

Se você criar o cluster com VLANs públicas e privadas, não será possível remover posteriormente todas as VLANs públicas desse cluster. A remoção de todas as VLANs públicas de um cluster faz com que diversos componentes do cluster parem de funcionar. Em vez disso, crie um novo conjunto de trabalhadores que esteja conectado a somente uma VLAN privada.
{: note}

É possível escolher permitir a comunicação de trabalhador para principal e de usuário para principal pelas redes públicas e privadas ou somente pela rede pública.
* Terminais em serviço público e privado: sua conta deve ser ativada com o VRF e ativada para usar os terminais em serviço. A comunicação entre os nós do trabalhador e o principal é estabelecida pela rede privada por meio do terminal em serviço privado e pela rede pública por meio do terminal em serviço público. O mestre é publicamente acessível aos usuários de cluster autorizados por meio do terminal em serviço público.
* Terminal em serviço público: se você não desejar ou não puder ativar o VRF para sua conta, seus nós do trabalhador e usuários do cluster autorizados poderão se conectar automaticamente ao principal do Kubernetes pela rede pública por meio do terminal em serviço público.

Os nós do trabalhador podem se comunicar de forma segura com outros serviços do {{site.data.keyword.cloud_notm}} que suportam terminais em serviço privados por meio de sua rede privada da infraestrutura do IBM Cloud. Se um serviço do {{site.data.keyword.cloud_notm}} não suportar terminais em serviço privado, os trabalhadores poderão se comunicar de forma segura com os serviços pela rede pública. É possível bloquear as interfaces públicas ou privadas de nós do trabalhador usando políticas de rede do Calico para isolamento de rede pública ou de rede privada. Talvez seja necessário permitir acesso aos endereços IP públicos e privados dos serviços que você deseja usar nessas políticas de isolamento do Calico.

Para expor um app em seu cluster na Internet, é possível criar um serviço público de balanceador de carga de rede (NLB) ou balanceador de carga de aplicativo (ALB) do Ingress. É possível melhorar a segurança de seu cluster, criando um conjunto de nós do trabalhador que são rotulados como nós de borda. Os pods para serviços de rede pública são implementados nos nós de borda para que as cargas de trabalho de tráfego externo sejam isoladas para somente alguns trabalhadores em seu cluster. É possível controlar ainda mais o tráfego público para os serviços de rede que expõem seus apps criando políticas do Calico anteriores ao DNAT, tais como políticas de lista de desbloqueio e de lista de bloqueio.

Se os nós do trabalhador precisarem acessar os serviços em redes privadas fora da sua conta do {{site.data.keyword.cloud_notm}}, será possível configurar e implementar o serviço VPN IPSec do strongSwan em seu cluster ou alavancar os serviços {{site.data.keyword.cloud_notm}} {{site.data.keyword.cloud_notm}} Direct Link para se conectar a essas redes.

Pronto para iniciar com um cluster neste cenário? Depois de planejar suas configurações de [alta disponibilidade](/docs/containers?topic=containers-ha_clusters) e [nó do trabalhador](/docs/containers?topic=containers-planning_worker_nodes), consulte [Criando clusters](/docs/containers?topic=containers-clusters#cluster_prepare).

<br />


## Cenário: ampliar seu data center no local em um cluster na rede privada e incluir o acesso público limitado
{: #limited-public}

Neste cenário, você deseja executar cargas de trabalho em um cluster que são acessíveis para serviços, bancos de dados ou outros recursos em seu data center no local. No entanto, pode ser necessário fornecer acesso público limitado ao seu cluster e desejar assegurar que qualquer acesso público seja controlado e isolado em seu cluster. Por exemplo, pode ser necessário que seus trabalhadores acessem um serviço do {{site.data.keyword.cloud_notm}} que não suporta terminais em serviço privado e deve ser acessado pela rede pública. Ou, pode ser necessário fornecer acesso público limitado a um app que é executado em seu cluster.
{: shortdesc}

Para alcançar essa configuração de cluster, é possível criar um firewall [usando nós de borda e políticas de rede do Calico](#calico-pc) ou [usando um dispositivo de gateway](#vyatta-gateway).

### Usando nós de borda e políticas de rede do Calico
{: #calico-pc}

Permita conectividade pública limitada com seu cluster usando nós de borda como um gateway público e políticas de rede do Calico como um firewall público.
{: shortdesc}

<p>
<figure>
 <img src="images/cs_clusters_planning_calico.png" alt="Imagem de arquitetura para um cluster que usa nós de borda e políticas de rede do Calico para acesso público seguro"/>
 <figcaption>Arquitetura para um cluster que usa nós de borda e políticas de rede do Calico para acesso público seguro</figcaption>
</figure>
</p>

Com essa configuração, você cria um cluster conectando nós do trabalhador a somente uma VLAN privada. Sua conta deve ser ativada com o VRF e ativada para usar os terminais em serviço privado.

O mestre do OpenShift será acessível por meio do terminal de serviço privado se os usuários do cluster autorizados estiverem em sua rede privada do {{site.data.keyword.cloud_notm}} ou estiverem conectados à rede privada por meio de uma [conexão de VPN](/docs/infrastructure/iaas-vpn?topic=VPN-getting-started) ou [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link). No entanto, a comunicação com o mestre do Kubernetes por meio do terminal em serviço privado deve passar pelo intervalo de endereços IP <code>166.X.X.X</code>, que não é roteável por meio de uma conexão VPN ou por meio do {{site.data.keyword.cloud_notm}} Direct Link. É possível expor o terminal em serviço privado do mestre para os usuários do cluster usando um balanceador de carga de rede (NLB) privado. O NLB privado expõe o terminal em serviço privado do mestre como um intervalo interno de endereços IP <code>10.X.X.X</code> que os usuários podem acessar com a VPN ou com a conexão do {{site.data.keyword.cloud_notm}} Direct Link. Se você ativar apenas o terminal em serviço privado, será possível usar o painel do Kubernetes ou ativar temporariamente o terminal em serviço público para criar o NLB privado.

Em seguida, é possível criar um conjunto de nós do trabalhador que estão conectados a VLANs públicas e privadas e rotuladas como nós de borda. Os nós de borda podem melhorar a segurança de seu cluster, permitindo que somente alguns nós do trabalhador sejam acessados externamente e isolando a carga de trabalho de rede para esses trabalhadores.

Os nós do trabalhador podem se comunicar de forma segura com outros serviços do {{site.data.keyword.cloud_notm}} que suportam terminais em serviço privados por meio de sua rede privada da infraestrutura do IBM Cloud. Se um serviço do {{site.data.keyword.cloud_notm}} não suportar terminais em serviço privado, seus nós de borda que estão conectados a uma VLAN pública poderão se comunicar de forma segura com os serviços pela rede pública. É possível bloquear as interfaces públicas ou privadas de nós do trabalhador usando políticas de rede do Calico para isolamento de rede pública ou de rede privada. Talvez seja necessário permitir acesso aos endereços IP públicos e privados dos serviços que você deseja usar nessas políticas de isolamento do Calico.

Para fornecer acesso privado a um app em seu cluster, é possível criar um balanceador de carga de rede (NLB) ou um balanceador de carga de aplicativo (ALB) do Ingress privado para expor seu app somente para a rede privada. É possível bloquear todo o tráfego público para esses serviços de rede que expõem seus apps criando políticas pré-DNAT do Calico, tais como políticas para bloquear NodePorts públicos em nós do trabalhador. Se precisar fornecer acesso público limitado a um app em seu cluster, será possível criar um NLB ou um ALB público para expor o app. Em seguida, deve-se implementar seus apps nesses nós de borda para que os NLBs ou ALBs possam direcionar o tráfego público para seus pods de app. É possível controlar ainda mais o tráfego público para os serviços de rede que expõem seus apps criando políticas do Calico anteriores ao DNAT, tais como políticas de lista de desbloqueio e de lista de bloqueio. Os pods para os serviços de rede privada e pública são implementados nos nós de borda para que as cargas de trabalho de tráfego externo sejam restritas a somente alguns trabalhadores em seu cluster.  

Para acessar serviços de forma segura fora do {{site.data.keyword.cloud_notm}} e de outras redes no local, é possível configurar e implementar o serviço VPN IPSec do strongSwan em seu cluster. O pod do balanceador de carga do strongSwan implementa em um trabalhador no conjunto de borda, em que o pod estabelece uma conexão segura com a rede no local por meio de um túnel VPN criptografado pela rede pública. Como alternativa, é possível usar os serviços {{site.data.keyword.cloud_notm}} Direct Link para conectar seu cluster ao seu data center no local somente pela rede privada.

Pronto para iniciar com um cluster neste cenário? Depois de planejar suas configurações de [alta disponibilidade](/docs/containers?topic=containers-ha_clusters) e [nó do trabalhador](/docs/containers?topic=containers-planning_worker_nodes), consulte [Criando clusters](/docs/containers?topic=containers-clusters#cluster_prepare).

</br>

### Usando um dispositivo de gateway
{: #vyatta-gateway}

Permita conectividade pública limitada para seu cluster, configurando um dispositivo de gateway, como um Virtual Router Appliance (Vyatta), como um gateway público e um firewall.
{: shortdesc}

<p>
<figure>
 <img src="images/cs_clusters_planning_gateway.png" alt="Imagem de arquitetura para um cluster que usa um dispositivo de gateway para acesso público seguro"/>
 <figcaption>Arquitetura para um cluster que usa um dispositivo de gateway para acesso público seguro</figcaption>
</figure>
</p>

Se você configura os nós do trabalhador somente em uma VLAN privada e não deseja ou não pode ativar o VRF para sua conta, deve-se configurar um dispositivo de gateway para fornecer conectividade de rede entre seus nós do trabalhador e o principal pela rede pública. Por exemplo, você pode escolher configurar um [Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-about-the-vra) ou um [Fortigate Security Appliance](/docs/services/vmwaresolutions/services?topic=vmware-solutions-fsa_considerations).

É possível configurar seu dispositivo de gateway com políticas de rede customizada para fornecer segurança de rede dedicada para seu cluster e para detectar e corrigir a intrusão de rede. Ao configurar um firewall na rede pública, deve-se abrir as portas necessárias e os endereços IP privados para cada região para que o principal e os nós do trabalhador possam se comunicar. Se esse firewall também é configurado para a rede privada, deve-se também abrir as portas necessárias e os endereços IP privados para permitir a comunicação entre os nós do trabalhador e permitir que seu cluster acesse os recursos de infraestrutura pela rede privada. Deve-se também ativar o VLAN Spanning para sua conta para que as sub-redes possam rotear na mesma VLAN e entre VLANs.

Para conectar de forma segura seus nós do trabalhador e apps a uma rede no local ou serviços fora do {{site.data.keyword.cloud_notm}}, configure um terminal VPN IPSec em seu dispositivo de gateway e o serviço VPN IPSec do strongSwan em seu cluster para usar o terminal VPN do gateway. Se você não desejar usar o strongSwan, será possível configurar a conectividade VPN diretamente com o VRA.

Os nós do trabalhador podem se comunicar de forma segura com outros serviços do {{site.data.keyword.cloud_notm}} e serviços públicos fora do {{site.data.keyword.cloud_notm}} por meio de seu dispositivo de gateway. É possível configurar seu firewall para permitir o acesso aos endereços IP públicos e privados somente dos serviços que você deseja usar.

Para fornecer acesso privado a um app em seu cluster, é possível criar um balanceador de carga de rede (NLB) ou um balanceador de carga de aplicativo (ALB) do Ingress privado para expor seu app somente para a rede privada. Se precisar fornecer acesso público limitado a um app em seu cluster, será possível criar um NLB ou um ALB público para expor o app. Como todo o tráfego passa por seu firewall de dispositivo de gateway, é possível controlar o público e o tráfego público para os serviços de rede que expõem seus apps abrindo as portas do serviço e os endereços IP em seu firewall para permitir o tráfego de entrada para esses serviços.

Pronto para iniciar com um cluster neste cenário? Depois de planejar suas configurações de [alta disponibilidade](/docs/containers?topic=containers-ha_clusters) e [nó do trabalhador](/docs/containers?topic=containers-planning_worker_nodes), consulte [Criando clusters](/docs/containers?topic=containers-clusters#cluster_prepare).

<br />


## Cenário: ampliar seu data center no local para um cluster na rede privada
{: #private_clusters}

Neste cenário, você deseja executar cargas de trabalho em um cluster do {{site.data.keyword.containerlong_notm}}. No entanto, você deseja que essas cargas de trabalho sejam acessíveis somente para serviços, bancos de dados ou outros recursos em seu data center no local, como {{site.data.keyword.icpfull_notm}}. Suas cargas de trabalho do cluster podem precisar acessar alguns outros serviços do {{site.data.keyword.cloud_notm}} que suportam comunicação pela rede privada, como {{site.data.keyword.cos_full_notm}}.
{: shortdesc}

<p>
<figure>
 <img src="images/cs_clusters_planning_extend.png" alt="Imagem de arquitetura para um cluster que se conecta a um data center no local na rede privada"/>
 <figcaption>Arquitetura para um cluster que se conecta a um data center no local na rede privada</figcaption>
</figure>
</p>

Para alcançar essa configuração, você cria um cluster conectando os nós do trabalhador a somente uma VLAN privada. Para fornecer conectividade entre o cluster principal e os nós do trabalhador pela rede privada por meio somente do terminal em serviço privado, sua conta deve ser ativada com o VRF e ativada para usar os terminais em serviço. Como seu cluster está visível a qualquer recurso na rede privada quando o VRF é ativado, é possível isolar seu cluster de outros sistemas na rede privada, aplicando políticas de rede privada do Calico.

O mestre do OpenShift será acessível por meio do terminal de serviço privado se os usuários do cluster autorizados estiverem em sua rede privada do {{site.data.keyword.cloud_notm}} ou estiverem conectados à rede privada por meio de uma [conexão de VPN](/docs/infrastructure/iaas-vpn?topic=VPN-getting-started) ou [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link). No entanto, a comunicação com o mestre do Kubernetes por meio do terminal em serviço privado deve passar pelo intervalo de endereços IP <code>166.X.X.X</code>, que não é roteável por meio de uma conexão VPN ou por meio do {{site.data.keyword.cloud_notm}} Direct Link. É possível expor o terminal em serviço privado do mestre para os usuários do cluster usando um balanceador de carga de rede (NLB) privado. O NLB privado expõe o terminal em serviço privado do mestre como um intervalo interno de endereços IP <code>10.X.X.X</code> que os usuários podem acessar com a VPN ou com a conexão do {{site.data.keyword.cloud_notm}} Direct Link. Se você ativar apenas o terminal em serviço privado, será possível usar o painel do Kubernetes ou ativar temporariamente o terminal em serviço público para criar o NLB privado.

Os nós do trabalhador podem se comunicar automaticamente com outros serviços do {{site.data.keyword.cloud_notm}} que suportam terminais em serviço privados, como o {{site.data.keyword.registrylong}}, por meio da rede privada de infraestrutura do IBM Cloud. Por exemplo, ambientes de hardware dedicados para todas as instâncias do plano padrão do {{site.data.keyword.cloudant_short_notm}} suportam terminais em serviço privado. Se um serviço do {{site.data.keyword.cloud_notm}} não suportar terminais em serviço privado, seu cluster não poderá acessar esse serviço.

Para fornecer acesso privado a um app em seu cluster, é possível criar um balanceador de carga de rede (NLB) ou balanceador de carga do aplicativo (ALB) do Ingress privado. Esses serviços de rede do Kubernetes expõem seu app somente à rede privada para que qualquer sistema no local com uma conexão à sub-rede em que o IP do NLB esteja possa acessar o aplicativo.

Pronto para iniciar com um cluster neste cenário? Depois de planejar suas configurações de [alta disponibilidade](/docs/containers?topic=containers-ha_clusters) e [nó do trabalhador](/docs/containers?topic=containers-planning_worker_nodes), consulte [Criando clusters](/docs/containers?topic=containers-clusters#cluster_prepare).


