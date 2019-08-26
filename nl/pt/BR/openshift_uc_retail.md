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

# Casos de Uso de Varejo para  {{site.data.keyword.cloud_notm}}
{: #cs_uc_retail}

Esses casos de uso destacam como as cargas de trabalho no {{site.data.keyword.openshiftlong}} podem
aproveitar de analítica para insights de mercado, implementações multiregion no mundo inteiro e gerenciamento de inventário com {{site.data.keyword.messagehub_full}} e armazenamento de objeto.
{: shortdesc}

## Um varejista de loja física compartilha dados, usando APIs, com parceiros de negócios globais para impulsionar as vendas de omnichannel
{: #uc_data-share}

Um Exec de Linha de Negócios (LOB) precisa aumentar os canais de vendas, mas o sistema de varejo é encerrado em um data center no local. A concorrência tem parceiros de negócios globais para permutações de venda cruzada e ampliada de suas mercadorias em locais físico e on-line. 
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: o Red Hat OpenShift on IBM Cloud fornece um ecossistema de nuvem pública, no qual os contêineres permitem que novos parceiros de negócios e outros players externos codesenvolvam apps e dados, por meio de APIs. Agora que o sistema de varejo está na nuvem pública, as APIs também aperfeiçoam o compartilhamento de dados e iniciam um novo desenvolvimento de aplicativo. As implementações de app aumentam quando os Desenvolvedores experimentam facilmente, enviando por push as mudanças para os sistemas de Desenvolvimento e Teste rapidamente com cadeias de ferramentas.

Red Hat OpenShift on IBM Cloud e principais tecnologias:
* [Clusters que se ajustam às necessidades variadas de CPU, RAM e armazenamento](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [{{site.data.keyword.cos_full}} para persistir e sincronizar dados entre os apps](/docs/tutorials?topic=solution-tutorials-pub-sub-object-storage#pub-sub-object-storage)
* [Ferramentas nativas do DevOps, incluindo cadeias de ferramentas abertas no {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)

**Contexto: o varejista compartilha dados, usando APIs, com parceiros de negócios globais para impulsionar as vendas de omnichannel**

* O varejista é confrontado com fortes pressões competitivas. Em primeiro lugar, eles precisam mascarar a complexidade da passagem para novos produtos e novos canais. Por exemplo, eles precisam expandir a sofisticação do produto. Ao mesmo tempo, isso precisa ser mais simples para seus clientes saltarem entre as marcas.
* Essa capacidade de alternar entre marcas significa que o ecossistema de varejo requer conectividade com parceiros de negócios. Em seguida, a nuvem pode fornecer um novo valor de parceiros de negócios, clientes e outros agentes externos.
* Os eventos de usuário de burst, como o Black Friday, pressionam os sistemas on-line existentes, forçando o varejista a superprovisionar a infraestrutura de cálculo.
* Os desenvolvedores do varejista precisavam desenvolver apps constantemente, mas as ferramentas tradicionais desaceleraram sua capacidade de implementar atualizações e recursos frequentemente, especialmente quando colaboram com as equipes de parceiros de negócios.  

** A Solução **

Uma experiência de compra mais inteligente é necessária para aumentar a retenção do cliente e a margem de lucro bruto. O modelo de vendas tradicional do varejista estava sofrendo devido à falta de inventário de parceiro de negócios para vendas cruzadas e vendas novas. Seus compradores estão procurando por conveniência maior, para que eles possam localizar itens relacionados rapidamente, como calças e tapetes de ioga.

O varejista também deve fornecer aos clientes conteúdo útil, como informações do produto, informações alternativas do produto, avaliações e visibilidade de inventário em tempo real. E esses clientes desejam isso enquanto estão on-line e na loja por meio de dispositivos móveis pessoais e associados à loja equipados com dispositivos móveis.

A solução é composta por estes componentes primários:
* INVENTÁRIO: um aplicativo para o ecossistema de parceiros de negócios que agrega e comunica o inventário, especialmente novas introduções de produto, incluindo APIs, para parceiros de negócios reutilizarem em seus próprios aplicativos de varejo e B2B
* VENDAS CRUZADAS E AMPLIADAS: app que exibe as oportunidades de venda cruzada e de venda ampliada com APIs que podem ser usadas em vários apps de e-commerce e móveis
* AMBIENTE DE DESENVOLVIMENTO: clusters Kubernetes para sistemas de Desenvolvimento, Teste e Produção aumentam a colaboração e o compartilhamento de dados entre o varejista e seus parceiros de negócios

Para que o varejista trabalhasse com parceiros de negócios globais, as APIs de inventário precisavam de mudanças de ajuste às preferências de idioma e mercado de cada região. O Red Hat OpenShift on IBM Cloud oferece cobertura em várias regiões, incluindo América do Norte, Europa, Ásia e Austrália, para que as APIs reflitam as necessidades de cada país e assegurem a baixa latência de chamadas de API.

Outro requisito é que os dados do inventário devem ser compartilháveis com os parceiros de negócios e clientes da empresa. Com as APIs de inventário, os Desenvolvedores podem obter informações em apps, como apps de inventário de dispositivo móvel ou soluções de e-commerce da web. Os Desenvolvedores também estão ocupados com a construção e a manutenção do site de e-commerce primário. Em resumo, eles precisam focar na codificação em vez de gerenciar a infraestrutura.

Dessa forma, eles escolheram o Red Hat OpenShift on IBM Cloud porque a IBM simplifica o gerenciamento de infraestrutura:
* Gerenciando os componentes principais, IaaS e operacionais do Kubernetes, como Ingress e armazenamento
* Monitorando o funcionamento e a recuperação de nós do trabalhador
* Fornecendo cálculo global, assim os Desenvolvedores possuem infraestrutura de hardware em regiões em que eles precisam que cargas de trabalho e dados residam

Além disso, a criação de log e o monitoramento para os microsserviços de API, especialmente como eles fazem pull de dados personalizados de sistemas de back-end, integram-se facilmente ao Red Hat OpenShift on IBM Cloud. Os desenvolvedores não perdem tempo construindo sistemas de criação de log complexos, apenas para solucionar problemas de sistemas em tempo real.

O {{site.data.keyword.messagehub_full}} atua como a plataforma de eventos no momento exato para fornecer as informações em constante mudança dos sistemas de inventário dos parceiros de negócios para o {{site.data.keyword.cos_full}}.

** Modelo de Solução **

O cálculo, o armazenamento e o gerenciamento de eventos sob demanda que são executados em nuvem pública com acesso a inventários de varejo no mundo inteiro, conforme necessário

Solução Técnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.messagehub_full}}
* {{site.data.keyword.cos_full}}
* {{site.data.keyword.contdelivery_full}}
* IBM Cloud Logging and Monitoring
* {{site.data.keyword.appid_short_notm}}

**Etapa 1: conteinerizar apps usando microsserviços**
* Estruture apps em um conjunto de microsserviços cooperativos que são executados no Red Hat OpenShift on IBM Cloud com base em áreas funcionais do app e suas dependências.
* Implemente apps em imagens de contêiner que são executadas no Red Hat OpenShift on IBM Cloud.
* Forneça painéis padronizados do DevOps por meio do Kubernetes.
* Ative o ajuste de escala sob demanda de cálculo para lote e outras cargas de trabalho de inventário que são executadas com pouca frequência.

** Etapa 2: assegure-se de disponibilidade global **
* As ferramentas de HA integradas no Red Hat OpenShift on IBM Cloud equilibram a carga de trabalho dentro de cada região geográfica, incluindo a capacidade de recuperação automática e o balanceamento de carga.
* O balanceamento de carga, os firewalls e o DNS são manipulados pelo IBM Cloud Internet Services.
* Usando as cadeias de ferramentas e as ferramentas de implementação do Helm, os apps também são implementados em clusters no mundo inteiro, portanto, as cargas de trabalho e os dados atendem aos requisitos regionais, especialmente a personalização.

**Etapa 3: Entender Usuários**
* O {{site.data.keyword.appid_short_notm}} fornece recursos de conexão sem a necessidade de mudar o código do app.
* Após os usuários terem se conectado, será possível usar o {{site.data.keyword.appid_short_notm}} para criar perfis e personalizar a experiência de um usuário de seu aplicativo.

** Etapa 4: Compartilhar dados **
* O {{site.data.keyword.cos_full}}, com o {{site.data.keyword.messagehub_full}}, fornece armazenamento de dados históricos e em tempo real para que as ofertas de vendas cruzadas representem o inventário disponível dos parceiros de negócios.
* As APIs permitem que os parceiros de negócios do varejista compartilhem dados em seus aplicativos de e-commerce e B2B.

** Etapa 5: Entregar continuamente **
* A depuração das APIs desenvolvidas em conjunto se torna mais simples quando elas incluem as ferramentas IBM Cloud Logging and Monitoring, aquelas baseadas em nuvem que estão acessíveis para os vários Desenvolvedores.
* O {{site.data.keyword.contdelivery_full}} ajuda os desenvolvedores a provisionar rapidamente uma cadeia de ferramentas integrada usando modelos customizáveis e compartilháveis com ferramentas da IBM, de terceiros e de software livre. Automatize construções e testes, controlando a qualidade com a análise de dados.
* Depois que os Desenvolvedores constroem e testam os apps em seus clusters de Desenvolvimento e Teste, eles usam as cadeias de ferramentas de integração e entrega contínuas da IBM (CI e CD) para implementar apps em clusters no mundo inteiro.
* O Red Hat OpenShift on IBM Cloud fornece fácil lançamento e retrocesso de apps; os apps customizados são implementados para testar campanhas por meio do roteamento inteligente e do balanceamento de carga do Istio.

** Resultados **
* Os microsserviços reduzem muito o tempo de entrega de correções, correções de bug e novos recursos. O desenvolvimento mundial inicial é rápido, e as atualizações são tão frequentes quanto 40 vezes por semana.
* O varejista e seus parceiros de negócios têm acesso imediato à disponibilidade do inventário e aos planejamentos de entrega por meio das APIs.
* Com o Red Hat OpenShift on IBM Cloud e as ferramentas IBM CI e CD, as versões A-B dos apps estão prontas para testar as campanhas.
* O Red Hat OpenShift on IBM Cloud fornece cálculo escalável, para que as cargas de trabalho de inventário e de API de vendas cruzadas possam crescer durante períodos de alto volume do ano, como os feriados de outono.

## O merceeiro tradicional aumenta o tráfego do cliente e as vendas com insights digitais
{: #uc_grocer}

Um Diretor de Marketing (CMO) precisa aumentar o tráfego de clientes em 20% nas lojas, tornando as lojas um recurso diferenciado. Os grandes concorrentes de varejo e os varejistas on-line estão roubando vendas. Ao mesmo tempo, a CMO precisa reduzir o inventário sem redução de preço porque manter o inventário por muito tempo empata milhões em capital.
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: o Red Hat OpenShift on IBM Cloud fornece fácil spin-up de mais cálculo, no qual os Desenvolvedores incluem rapidamente serviços de Cloud Analytics para insights de comportamento de vendas e adaptabilidade do mercado digital.

Tecnologias chave:    
* [ Escalonamento horizontal para acelerar o desenvolvimento ](/docs/containers?topic=containers-app#highly_available_apps)
* [Clusters que se ajustam às necessidades variadas de CPU, RAM e armazenamento](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Insights para tendências de mercado com o Watson Discovery](https://www.ibm.com/watson/services/discovery/)
* [Ferramentas nativas do DevOps, incluindo cadeias de ferramentas abertas no {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [ Gerenciamento de Inventário com o  {{site.data.keyword.messagehub_full}} ](/docs/services/EventStreams?topic=eventstreams-about#about)

**Contexto: o merceeiro tradicional aumenta o tráfego de clientes e as vendas com insights digitais**

* As pressões competitivas de varejistas on-line e grandes lojas de varejo interromperam os modelos tradicionais de varejo de mercearia. As vendas estão declinando, evidenciadas pelo baixo tráfego de pedestres em lojas físicas.
* Seus programas de fidelidade precisam de um impulsionamento com um toque moderno nos cupons impressos no check-out. Portanto, os Desenvolvedores devem desenvolver constantemente os apps relacionados, mas as ferramentas tradicionais desaceleram a sua capacidade de implementar atualizações e recursos frequentemente.  
* Determinado inventário de alto valor não está se movendo tão bem quanto o esperado, mas ainda assim o movimento "gourmet" parece estar crescendo em grandes mercados metropolitanos.

** A Solução **

O merceeiro precisa de um app para aumentar a conversão e armazenar o tráfego para gerar novas vendas e construir a fidelidade do cliente em uma plataforma de análise de nuvem reutilizável. A experiência com alvo dentro da loja pode ser um evento junto com um fornecedor de serviços ou produto que atraia fidelidade e novos clientes com base na afinidade com o evento específico. Em seguida, a loja e o parceiro de negócios oferecem incentivos para o comparecimento ao evento e a possibilidade de compra de produtos da loja ou do parceiro de negócios.  

Após o evento, os clientes são orientados a comprar os produtos necessários, para que eles possam repetir a atividade demonstrada sozinhos no futuro. A experiência de cliente-alvo é medida com o resgate de incentivo e as novas inscrições de clientes de fidelidade. A combinação de um evento de marketing hiperpersonalizado e uma ferramenta para rastrear compras dentro da loja pode conduzir a experiência-alvo por toda a compra do produto. Todas essas ações resultam em tráfego mais alto e conversões.

Como um evento de exemplo, um chef local é trazido para a loja para mostrar como fazer uma refeição gourmet. A loja fornece um incentivo para impulsionar a participação. Por exemplo, eles fornecem um aperitivo grátis no restaurante do chef e um incentivo extra para comprar os ingredientes para a refeição demonstrada (por exemplo, $20 de desconto no carrinho de compras de $150).

A solução é composta por estes componentes primários:
1. ANÁLISE DE INVENTÁRIO: os eventos dentro da loja (receitas, listas de ingredientes e localizações de produtos) são customizados para comercializar o inventário com movimentação lenta.
2. O APP MÓVEL DE FIDELIDADE fornece marketing direcionado com cupons digitais, listas de compras, inventário de produto (preços, disponibilidade) em um mapa de loja e compartilhamento social.
3. O SOCIAL MEDIA ANALYTICS fornece a personalização, detectando as preferências dos clientes em termos de tendências: gastronomia, chefs e ingredientes. A análise conecta tendências regionais a uma atividade do Twitter, Pinterest e Instagram do indivíduo.
4. As FERRAMENTAS AMIGÁVEIS PARA O DESENVOLVEDOR aceleram o lançamento de recursos e as correções de bug.

Os sistemas de inventário de backend para inventário do produto, reabastecimento de loja e previsão de produtos têm uma grande quantidade de informações, mas a análise moderna pode desbloquear novos insights sobre como mover melhor os produtos de alta tecnologia. Usando uma combinação do {{site.data.keyword.cloudant}} e do IBM Streaming Analytics, o CMO pode localizar o ponto ideal dos ingredientes para corresponder aos eventos customizados dentro da loja.

O {{site.data.keyword.messagehub_full}} age como a plataforma de eventos no momento exato para trazer as informações de rápida mudança dos sistemas de inventário para o IBM Streaming Analytics.

As análises de mídia social com o Watson Discovery (insights de personalidade e tom) também alimentam tendências para a análise de inventário para melhorar a previsão do produto.

O app móvel de fidelidade fornece informações detalhadas de personalização, especialmente quando os clientes usam seus recursos de compartilhamento social, como postagem de receitas.

Além do app móvel, os Desenvolvedores estão ocupados com a construção e a manutenção do aplicativo de fidelidade existente que está ligado aos cupons de check-out tradicionais. Em resumo, eles precisam focar na codificação em vez de gerenciar a infraestrutura. Dessa forma, eles escolheram o Red Hat OpenShift on IBM Cloud porque a IBM simplifica o gerenciamento de infraestrutura:
* Gerenciando os componentes principais, IaaS e operacionais do Kubernetes, como Ingress e armazenamento
* Monitorando o funcionamento e a recuperação de nós do trabalhador
* Fornecendo cálculo global, assim os Desenvolvedores não são responsáveis pela configuração de infraestrutura em datacenters

** Modelo de Solução **

O cálculo, o armazenamento e o gerenciamento de eventos sob demanda que são executados em nuvem pública com acesso a sistemas ERP de backend

Solução Técnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.messagehub_full}}
* {{site.data.keyword.cloudant}}
* IBM Streaming Analytics
* IBM Watson Discovery

**Etapa 1: conteinerizar apps usando microsserviços**

* Estruture a análise de inventário e os apps móveis em microsserviços e os implemente em contêineres no Red Hat OpenShift on IBM Cloud.
* Forneça painéis padronizados do DevOps por meio do Kubernetes.
* Escale o cálculo sob demanda para lote e outras cargas de trabalho de inventário que são executadas com menos frequência.

**Etapa 2: analisar o inventário e as tendências**
* O {{site.data.keyword.messagehub_full}} age como a plataforma de eventos no momento exato para trazer as informações de rápida mudança de sistemas de inventário para o IBM Streaming Analytics.
* A análise de mídia social com dados do Watson Discovery e de sistemas de inventário é integrada ao IBM Streaming Analytics para entregar aconselhamento de merchandise e marketing.

**Etapa 3: entregar promoções com app de fidelidade móvel**
* Impulsione o desenvolvimento de app móvel com o IBM Mobile Starter Kit e outros serviços IBM Mobile, como {{site.data.keyword.appid_full_notm}}.
* As promoções na forma de cupons e outras titularidades são enviadas para o app móvel dos usuários. As promoções foram identificadas usando o inventário e a análise social, além de outros sistemas de backend.
* O armazenamento de receitas de promoção em app móvel e conversões (cupons de check-out resgatados) são alimentados de volta para sistemas ERP para análise adicional.

** Resultados **
* Com o Red Hat OpenShift on IBM Cloud, os microsserviços reduzem muito o tempo para a entrega de correções, correções de erros e novos recursos. O desenvolvimento inicial é rápido e as atualizações são frequentes.
* O tráfego de clientes e as vendas aumentaram em lojas, tornando as próprias lojas um recurso diferenciado.
* Ao mesmo tempo, novos insights de análise social e cognitiva melhoraram o inventário reduzido OpEx (despesas operacionais).
* O compartilhamento social no app móvel também ajuda a identificar e comercializar para novos clientes.


