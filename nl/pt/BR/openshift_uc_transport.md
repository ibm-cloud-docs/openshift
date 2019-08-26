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

# Casos de uso de transporte para  {{site.data.keyword.cloud_notm}}
{: #cs_uc_transport}

Esses casos de uso destacam como as cargas de trabalho no {{site.data.keyword.openshiftlong}} podem
aproveitar as cadeias de ferramentas para rápidas atualizações de app e implementações multiregion no mundo inteiro. Ao mesmo tempo, essas cargas de trabalho podem se conectar a sistemas de backend existentes, usar o Watson AI para personalização e acessar dados IoT com o {{site.data.keyword.messagehub_full}}.

{: shortdesc}

## A empresa de remessa aumenta a disponibilidade de sistemas mundiais para o ecossistema de parceiros de negócios
{: #uc_shipping}

Um executivo de TI tem sistemas de planejamento e de roteamento de remessa em todo o mundo com os quais os parceiros interagem Os parceiros requerem informações atualizadas desses sistemas que acessam dados do dispositivo IoT. Mas, esses sistemas não eram capazes de escalar no mundo inteiro com HA suficiente. 
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: o Red Hat OpenShift on IBM Cloud escala apps conteinerizados com cinco 9s de disponibilidade para atender às crescentes demandas. As implementações de app ocorrem 40 vezes diariamente quando os Desenvolvedores experimentam facilmente, enviando por push as mudanças para os sistemas de Desenvolvimento e Teste rapidamente. A Plataforma IoT torna fácil o acesso a dados do IoT.

Tecnologias chave:    
* [ Multi-regiões para o ecossistema de parceiro de negócios  ](/docs/containers?topic=containers-regions-and-zones#regions-and-zones)
* [ Escalação Horizontal ](/docs/containers?topic=containers-app#highly_available_apps)
* [ Abrir cadeias de ferramentas no  {{site.data.keyword.contdelivery_full}} ](https://www.ibm.com/cloud/garage/toolchains/)
* [ Serviços de nuvem para inovação ](https://www.ibm.com/cloud/products/#analytics)
* [{{site.data.keyword.messagehub_full}} para alimentar dados do evento para apps](/docs/services/EventStreams?topic=eventstreams-about#about)

**Contexto: A empresa de remessa aumenta a disponibilidade de sistemas mundiais para o ecossistema de parceiros de negócios**

* As diferenças regionais para a logística de remessa tornaram difícil acompanhar o número crescente de parceiros em múltiplos países. Um exemplo é a regulamentação exclusiva e a logística de trânsito, em que a empresa deve manter registros consistentes entre as fronteiras.
* Dados no momento exato significam que os sistemas mundiais devem estar altamente disponíveis para reduzir atrasos em operações de trânsito. Os cronogramas para terminais de remessa são altamente controladas e, em alguns casos, inflexíveis. O uso da web está aumentando, portanto, a instabilidade pode causar uma experiência do usuário insatisfatória.
* Os desenvolvedores precisavam desenvolver apps constantemente, mas as ferramentas tradicionais desaceleravam sua capacidade de implementar atualizações e recursos frequentemente.  

** A Solução **

A companhia de navegação precisa gerenciar cronogramas de remessa, inventários e documentação de alfândega de maneira coesa. Então, eles podem compartilhar com precisão o local de remessas, conteúdos de remessa e planejamentos de entrega para seus clientes. Eles estão fazendo o trabalho de adivinhação de quando uma mercadoria (como um dispositivo, roupa ou produto) chegará para que seus clientes de remessa possam comunicar essas informações para seus próprios clientes.

A solução é composta por estes componentes primários:
1. Dados de fluxo de dispositivos IoT para cada contêiner de remessa: manifests e local
2. A documentação de alfândega que é compartilhada digitalmente com portos e parceiros de trânsito aplicáveis, incluindo controle de acesso
3. O app para clientes de remessa que agrega e comunica informações de chegada para mercadorias enviadas, incluindo APIs para clientes de remessa para reutilização de dados de remessa em seus próprios apps de varejo e entre empresas

Para que a companhia de navegação trabalhe com parceiros globais, os sistemas de roteamento e planejamento exigiram modificações locais para ajustar ao idioma, às regulamentações e à logística exclusiva do porto de cada região. O Red Hat OpenShift on IBM Cloud oferece cobertura global em várias regiões, incluindo América do Norte, Europa, Ásia e Austrália, para que os apps reflitam as necessidades de seus parceiros, em cada país.

Os dispositivos IoT transmitem dados que o {{site.data.keyword.messagehub_full}} distribui para os apps de portos regionais e os armazenamentos de dados de manifest de Alfândega e Contêiner associados. {{site.data.keyword.messagehub_full}}  é o ponto de entrada para eventos IoT. Ele distribui os eventos com base na conectividade gerenciada que o Watson IoT Platform oferece ao {{site.data.keyword.messagehub_full}}.

Após os eventos estarem no {{site.data.keyword.messagehub_full}}, eles são persistidos para uso imediato nos apps de trânsito do porto e para qualquer ponto no futuro. Os apps que requerem a latência mais baixa consomem diretamente em tempo real do fluxo do evento ({{site.data.keyword.messagehub_full}}). Outros apps futuros, como ferramentas de análise, podem escolher consumir em um modo de lote por meio do armazenamento de eventos com o {{site.data.keyword.cos_full}}.

Como os dados de navegação são compartilhados com os clientes da empresa, os Desenvolvedores garantem que os clientes possam usar APIs para recebê-los em seus próprios aplicativos. Exemplos desses apps são aplicativos de rastreamento móvel ou soluções de e-commerce da web. Os Desenvolvedores também estão ocupados com a construção e a manutenção dos apps de portos regionais que reúnem e disseminam os registros de alfândega e os manifests de remessa. Em resumo, eles precisam focar na codificação em vez de gerenciar a infraestrutura. Dessa forma, eles escolheram o Red Hat OpenShift on IBM Cloud porque a IBM simplifica o gerenciamento de infraestrutura:
* Gerenciando os componentes principais, IaaS e operacionais do Kubernetes, como Ingress e armazenamento
* Monitorando o funcionamento e a recuperação de nós do trabalhador
* Fornecendo cálculo global, assim os desenvolvedores não são responsáveis pela infraestrutura em várias regiões em que eles precisam que cargas de trabalho e dados residam

Para alcançar a disponibilidade global, os sistemas de Desenvolvimento, Teste e Produção foram implementados no mundo inteiro em vários data centers. Para HA, eles usam uma combinação de múltiplos clusters em diferentes regiões geográficas, bem como clusters de múltiplas zonas. Eles podem implementar facilmente o app de porto para atender às necessidades de negócios:
* Em clusters de Frankfurt para obedecer às regulamentações europeias locais
* Nos clusters dos Estados Unidos para assegurar a disponibilidade local e a recuperação de falha

Eles também difundem a carga de trabalho entre clusters de múltiplas zonas em Frankfurt para assegurar que a versão europeia do app esteja disponível, além de equilibrar a carga de trabalho de maneira eficiente. Como cada região faz o upload de dados exclusivos com o app de porto, os clusters do app são hospedados em regiões em que a latência é baixa.

Para Desenvolvedores, grande parte do processo de integração e entrega contínuas (CI/CD) pode ser automatizado com o {{site.data.keyword.contdelivery_full}}. A empresa pode definir as cadeias de ferramentas de fluxo de trabalho para preparar imagens de contêiner, verificar vulnerabilidades e implementá-las no cluster do Kubernetes.

** Modelo de Solução **

O cálculo, o armazenamento e o gerenciamento de eventos sob demanda que são executados em nuvem pública com acesso a dados de remessa no mundo inteiro, conforme necessário

Solução Técnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.messagehub_full}}
* {{site.data.keyword.cos_full}}
* {{site.data.keyword.contdelivery_full}}

**Etapa 1: conteinerizar apps usando microsserviços**

* Integre os apps em um conjunto de microsserviços cooperativos no Red Hat OpenShift on IBM Cloud com base em áreas funcionais do app e suas dependências.
* Implemente os apps em contêineres no Red Hat OpenShift on IBM Cloud.
* Forneça painéis padronizados do DevOps por meio do Kubernetes.
* Ative o ajuste de escala sob demanda de cálculo para lote e outras cargas de trabalho de inventário que são executadas com pouca frequência.
* Use o {{site.data.keyword.messagehub_full}} para gerenciar dados de fluxo de dispositivos IoT.

** Etapa 2: assegure-se de disponibilidade global **
* As ferramentas de HA integradas no Red Hat OpenShift on IBM Cloud equilibram a carga de trabalho dentro de cada região geográfica, incluindo a capacidade de recuperação automática e o balanceamento de carga.
* O balanceamento de carga, os firewalls e o DNS são manipulados pelo IBM Cloud Internet Services.
* Usando as cadeias de ferramentas e as ferramentas de implementação do Helm, os apps também são implementados em clusters no mundo inteiro, portanto, as cargas de trabalho e os dados atendem aos requisitos regionais.

** Etapa 3: Compartilhar dados **
* O {{site.data.keyword.cos_full}} e o {{site.data.keyword.messagehub_full}} fornecem armazenamento de dados em tempo real e em histórico.
* As APIs permitem que os clientes da companhia de navegação compartilhem dados em seus aplicativos.

** Etapa 4: Entregar continuamente **
* O {{site.data.keyword.contdelivery_full}} ajuda os desenvolvedores a provisionarem rapidamente uma cadeia de ferramentas integrada, usando modelos customizáveis, compartilháveis com ferramentas da IBM, de terceiros e de software livre. Automatize construções e testes, controlando a qualidade com a análise de dados.
* Depois que os Desenvolvedores constroem e testam os apps em seus clusters de Desenvolvimento e teste, eles usam as cadeias de ferramentas CI/CD da IBM para implementar apps nos clusters em todo o globo.
* O Red Hat OpenShift on IBM Cloud fornece fácil lançamento e retrocesso de apps; os apps customizados são implementados para atender aos requisitos regionais por meio de um roteamento inteligente e balanceamento de carga do Istio.

** Resultados **

* Com o Red Hat OpenShift on IBM Cloud e as ferramentas IBM CI/CD, as versões regionais dos apps são hospedadas próximas dos dispositivos físicos dos quais reúnem dados.
* Os microsserviços reduzem muito o tempo de entrega de correções, correções de bug e novos recursos. O desenvolvimento inicial é rápido e as atualizações são frequentes.
* Os clientes de remessa têm acesso em tempo real para locais de remessas, planejamentos de entrega e até registros de porto aprovados.
* Os parceiros de trânsito em vários terminais de remessa estão cientes dos manifests e detalhes da remessa para que as logísticas no local sejam melhoradas, em vez de atrasadas.
* Separadamente desta história, a [Maersk e a IBM formaram uma joint venture](https://www.ibm.com/press/us/en/pressrelease/53602.wss) para melhorar as cadeias de suprimento internacionais com Blockchain.

## A companhia aérea entrega um site inovador de benefícios de Recursos Humanos (HR) em menos de 3 semanas
{: #uc_airline}

Um Exec de RH (CHRO) precisa de um novo site de benefícios de RH com um robô de bate-papo inovador, mas as ferramentas de desenvolvimento e a plataforma atuais significam tempos longos de preparação para que os apps fiquem ativos. Essa situação inclui esperas longas para compras de hardware.
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: Red Hat OpenShift on IBM Cloud fornece uma fácil aceleração de cálculo. Em seguida, os Desenvolvedores podem experimentar facilmente, enviando por push mudanças para sistemas de Desenvolvimento e teste rapidamente com cadeias de ferramentas abertas. Suas ferramentas de desenvolvimento de software tradicionais ganham impulso quando elas incluem o IBM Watson Assistant. O novo site de benefícios foi criado em menos de 3 semanas.

Tecnologias chave:    
* [Clusters que se ajustam às necessidades variadas de CPU, RAM e armazenamento](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [ Serviço de Chatbot desenvolvido com o Watson ](https://developer.ibm.com/code/patterns/create-cognitive-banking-chatbot/)
* [Ferramentas nativas do DevOps, incluindo cadeias de ferramentas abertas no {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [SDK for Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)

**Contexto: construindo e implementando rapidamente o site inovador de benefícios de RH em menos de 3 semanas**
* O crescimento dos funcionários e a mudança de políticas de RH significaram que um novo site inteiro seria necessário para a inscrição anual.
* Os recursos interativos, como um robô de bate-papo, devem ajudar a comunicar as novas políticas de RH aos funcionários existentes.
* Devido ao crescimento de número de funcionários, o tráfego do site está aumentando, mas o orçamento de infraestrutura permanece estável.
* A equipe de RH enfrentou pressão para se mover mais rápido: apresentar novos recursos do site rapidamente e postar mudanças de benefício de última hora frequentemente.
* O período de inscrição dura duas semanas e, portanto, o tempo de inatividade para o novo app não é tolerado.

** A Solução **

A companhia aérea deseja projetar uma cultura aberta que coloca as pessoas em primeiro plano. O executivo de RH está bem ciente de que o foco em recompensação e retenção de talentos afeta a lucratividade da companhia aérea. Assim, o lançamento anual de benefícios é um aspecto chave da estimação de uma cultura centrada no funcionário.

Eles precisam de uma solução que ajude os Desenvolvedores e seus usuários:
* FRONT-END PARA BENEFÍCIOS EXISTENTES: seguro, ofertas educacionais, bem-estar e muito mais
* RECURSOS ESPECÍFICOS DA REGIÃO: cada país tem políticas exclusivas de RH para que o site geral possa parecer semelhante, mas mostrar benefícios específicos da região
* FERRAMENTAS AMIGÁVEIS PARA O DESENVOLVEDOR que aceleram o lançamento de recursos e correções de bug
* ROBÔ DE BATE-PAPO para fornecer conversas autênticas sobre os benefícios e resolver solicitações e perguntas dos usuários de maneira eficiente.

Solução Técnica:
* Red Hat OpenShift on IBM Cloud
* IBM Watson Assistant e Tone Analyzer
* {{site.data.keyword.contdelivery_full}}
* IBM Logging and Monitoring
* {{site.data.keyword.SecureGatewayfull}}
* {{site.data.keyword.appid_full_notm}}

O desenvolvimento acelerado é uma vitória chave para o Exec de RH. A equipe começa conteinerizando seus apps e colocando-os na nuvem. Com o uso de contêineres modernos, os Desenvolvedores podem experimentar facilmente com o SDK do Node.js e enviar por push as mudanças para os sistemas de Desenvolvimento e Teste, que são escalados em clusters separados. Esses pushes foram automatizados com cadeias de ferramentas abertas e o {{site.data.keyword.contdelivery_full}}. As atualizações para o site de RH não mais se arrastam em processos de construção lentos e propensos a erros. Eles podem entregar atualizações incrementais para seu site, diariamente ou ainda mais frequentemente.  Além disso, a criação de log e o monitoramento para o site de RH são rapidamente integrados, especialmente em como o site puxa dados personalizados de sistemas de benefícios de backend. Os desenvolvedores não perdem tempo construindo sistemas de criação de log complexos, apenas para solucionar problemas de sistemas em tempo real. Os desenvolvedores não precisam se tornar especialistas em segurança de nuvem, pois podem aplicar a autenticação orientada por política facilmente por meio do {{site.data.keyword.appid_full_notm}}.

Com o Red Hat OpenShift on IBM Cloud, eles foram de hardware superconstruído em um data center privado para o cálculo customizável que reduz operações de TI, manutenção e energia. Para hospedar o site de RH, eles podem projetar facilmente os clusters do Kubernetes para ajustar suas necessidades de CPU, RAM e armazenamento. Outro fator para menos custos de equipe é que a IBM gerencia o Kubernetes, para que os Desenvolvedores possam se concentrar em entregar a melhor experiência do funcionário para a inscrição de benefícios.

O Red Hat OpenShift on IBM Cloud fornece recursos de cálculo escaláveis e os painéis do DevOps associados para criar, escalar e derrubar apps e serviços on demand. Usando a tecnologia de contêineres de padrão de mercado, os apps podem ser desenvolvidos e compartilhados rapidamente entre múltiplos ambientes de Desenvolvimento, Teste e Produção. Essa configuração fornece o benefício imediato de escalabilidade. Usando o conjunto rich do Kubernetes de objetos de implementação e de tempo de execução, a equipe do RH pode monitorar e gerenciar upgrades para apps de forma confiável. Eles também podem replicar e escalar os apps, usando regras definidas e o orquestrador automatizado do Kubernetes.

**Etapa 1: contêineres, microsserviços e o Garage Method**
* Os apps são construídos em um conjunto de microsserviços cooperativos que são executados no Red Hat OpenShift on IBM Cloud. A arquitetura representa as áreas funcionais do app com os problemas mais importantes.
* Implemente os apps no contêiner no Red Hat OpenShift on IBM Cloud, varrido continuamente com o IBM Vulnerability Advisor.
* Forneça painéis padronizados do DevOps por meio do Kubernetes.
* Adote as práticas de desenvolvimento agile e iterativas essenciais dentro do IBM Garage Method para ativar liberações frequentes de novas funções, correções e correções sem tempo de inatividade.

**Etapa 2: conexões com o backend de benefícios existentes**
* O {{site.data.keyword.SecureGatewayfull}} é usado para criar um túnel seguro para sistemas no local que hospedam os sistemas de benefícios.  
* A combinação de dados no local e o Red Hat OpenShift on IBM Cloud permite que eles acessem dados sensíveis enquanto aderem aos regulamentos.
* Conversas de robô de bate-papo alimentadas de volta para as políticas de RH, permitindo que o site de benefícios reflita quais benefícios foram mais e menos populares, incluindo melhorias direcionadas para iniciativas de baixo desempenho.

** Etapa 3: Chatbot e personalização **
* O IBM Watson Assistant fornece ferramentas para suportar rapidamente um robô de bate-papo que pode fornecer as informações corretas de benefícios para os usuários.
* O Watson Tone Analyzer assegura que os clientes estejam satisfeitos com as conversas do robô de bate-papo e façam a intervenção humana quando necessário.

**Etapa 4: entregar continuamente no mundo inteiro**
* O {{site.data.keyword.contdelivery_full}} ajuda os desenvolvedores a provisionarem rapidamente uma cadeia de ferramentas integrada, usando modelos customizáveis, compartilháveis com ferramentas da IBM, de terceiros e de software livre. Automatize construções e testes, controlando a qualidade com a análise de dados.
* Depois que os Desenvolvedores constroem e testam os apps em seus clusters de Desenvolvimento e Teste, eles usam as cadeias de ferramentas do IBM CI/CD para implementar apps em clusters de Produção no mundo inteiro.
* O Red Hat OpenShift on IBM Cloud fornece fácil lançamento e retrocesso de apps. Os aplicativos customizados são implementados para atender aos requisitos regionais por meio do roteamento inteligente e do balanceamento de carga do Istio.
* As ferramentas de HA integradas no Red Hat OpenShift on IBM Cloud equilibram a carga de trabalho dentro de cada região geográfica, incluindo a capacidade de recuperação automática e o balanceamento de carga.

** Resultados **
* Com ferramentas como o robô de bate-papo, a equipe de RH provou à sua mão de obra que a inovação era parte da cultura corporativa, não apenas meras palavras.
* A autenticidade com a personalização no site abordou as expectativas de mudança da mão de obra da companhia aérea hoje.
* As atualizações de última hora para o site de RH, incluindo aquelas que são guiadas pelas conversas de robô de bate-papo dos funcionários, entraram em ação rapidamente porque os Desenvolvedores estavam enviando por push as mudanças pelo menos 10 vezes diariamente.
* Com o gerenciamento de infraestrutura resolvido pela IBM, a equipe de Desenvolvimento foi liberada para entregar o site em somente 3 semanas.


