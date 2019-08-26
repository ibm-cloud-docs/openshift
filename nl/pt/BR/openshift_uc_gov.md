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

# Casos de uso do governo para  {{site.data.keyword.cloud_notm}}
{: #cs_uc_gov}

Esses casos de uso destacam como as cargas de trabalho no {{site.data.keyword.openshiftlong}} se beneficiam da nuvem pública. Essas cargas de trabalho são isoladas em regiões globais para a soberania de dados, usam o aprendizado de máquina do Watson em vez do código novo e se conectam aos bancos de dados no local.
{: shortdesc}

## O governo regional melhora a colaboração e a velocidade com os Desenvolvedores da comunidade que combinam dados públicos/privados
{: #uc_data_mashup}

Um Executivo de Programa de Dados de Governo Aberto precisa compartilhar dados públicos com a comunidade e o setor privado, mas os dados são bloqueados em um sistema monolítico no local. 
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: com o Red Hat OpenShift on IBM Cloud, o Exec entrega o valor transformador de dados públicos-privados combinados. Da mesma forma, o serviço fornece a plataforma de nuvem pública para refatorar e expor microsserviços por meio de apps monolíticos no local. Além disso, a nuvem pública permite que o governo e as parcerias públicas usem serviços de nuvem externa e ferramentas de software livre fáceis.

Tecnologias chave:    
* [Clusters que se ajustam às necessidades variadas de CPU, RAM e armazenamento](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Ferramentas nativas do DevOps, incluindo cadeias de ferramentas abertas no {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [ Fornecer acesso a dados públicos com o  {{site.data.keyword.cos_full_notm}} ](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage)
* [ Serviços do IBM Cloud Analytics Plug-and-play ](https://www.ibm.com/cloud/analytics)

**Contexto: o governo melhora a colaboração e a velocidade com os Desenvolvedores da comunidade que combinam dados públicos/privados**
* Um modelo de "governo aberto" é o futuro, mas essa agência do governo regional não pode dar o salto com seus sistemas no local.
* Eles desejam suportar a inovação e estimular o codesenvolvimento entre o setor privado, os cidadãos e as agências públicas.
* Os grupos distintos de Desenvolvedores do governo e das organizações privadas não têm uma plataforma de software livre unificada na qual eles podem compartilhar APIs e dados facilmente.
* Os dados do governo são bloqueados em sistemas no local sem acesso público fácil.

** A Solução **

Uma transformação de governo aberto deve ser construída em uma base que forneça desempenho, resiliência, continuidade de negócios e segurança. À medida que a inovação e o codesenvolvimento avançam, as agências e os cidadãos dependem de empresas de software, serviços e infraestrutura para “proteger e servir”.

Para acabar com a burocracia e transformar a relação do governo com seu eleitorado, eles se voltaram para padrões abertos para construir uma plataforma para a cocriação:

* DADOS ABERTOS - armazenamento de dados em que cidadãos, agências governamentais e negócios acessam, compartilham e aprimoram dados livremente
* APIs ABERTAS - uma plataforma de desenvolvimento em que as APIs são contribuídas e reutilizadas por todos os parceiros da comunidade
* INOVAÇÃO ABERTA - um conjunto de serviços de nuvem que permitem que os desenvolvedores conectem a inovação em vez de codificá-la manualmente

Para começar, o governo usa o {{site.data.keyword.cos_full_notm}} para armazenar seus dados públicos na nuvem. Esse armazenamento é grátis para usar e reutilizar, compartilhável por qualquer pessoa e sujeito somente a atribuição e compartilhamento semelhantes. Os dados sensíveis podem ser limpos antes de serem enviados por push para a nuvem. Além disso, os controles de acesso são configurados para que a nuvem capture o novo armazenamento de dados, em que a comunidade possa demonstrar POCs de dados grátis existentes aprimorados.

A próxima etapa do governo para as parcerias público-privadas é estabelecer uma economia de API que está hospedada no {{site.data.keyword.apiconnect_long}}. Lá, os desenvolvedores da comunidade e da empresa tornam os dados facilmente acessíveis no formato de API. Seus objetivos são ter APIs de REST disponíveis publicamente, para ativar a interoperabilidade e para acelerar a integração de apps. Eles usam o IBM {{site.data.keyword.SecureGateway}} para se conectar de volta às origens de dados privadas no local.

Por fim, os apps baseados nessas APIs compartilhadas são hospedados no Red Hat OpenShift on IBM Cloud, no qual é fácil girar os clusters. Em seguida, os Desenvolvedores na comunidade, no setor privado e no governo podem criar em conjunto apps facilmente. Em resumo, os Desenvolvedores precisam se concentrar na codificação em vez de gerenciar a infraestrutura. Dessa forma, eles escolheram o Red Hat OpenShift on IBM Cloud porque a IBM simplifica o gerenciamento de infraestrutura:
* Gerenciando os componentes principais, IaaS e operacionais do Kubernetes, como Ingress e armazenamento
* Monitorando o funcionamento e a recuperação de nós do trabalhador
* Fornecendo cálculo global, de modo que os Desenvolvedores não precisem se responsabilizar pela infraestrutura em várias regiões do mundo onde cargas de trabalho e dados precisem estar localizados

Mover as cargas de trabalho de cálculo para o {{site.data.keyword.cloud_notm}} não é o suficiente. O governo precisa passar por uma transformação de processo e métodos também. Adotando as práticas do IBM Garage Method, o provedor pode implementar um processo de entrega agile e iterativo que suporta práticas modernas do DevOps, como a Integração e Entrega Contínuas (CI/CD).

Grande parte do processo CI/CD em si é automatizado com o {{site.data.keyword.contdelivery_full}} na nuvem. O provedor pode definir cadeias de ferramentas de fluxo de trabalho para preparar imagens de contêiner, verificar vulnerabilidades e implementá-las no cluster do Kubernetes.

** Modelo de Solução **

As ferramentas de cálculo, armazenamento e API sob demanda são executadas na nuvem pública com acesso seguro para e de origens de dados no local.

Solução Técnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.cos_full_notm}} e o {{site.data.keyword.cloudant}}
* {{site.data.keyword.apiconnect_long}}
* IBM  {{site.data.keyword.SecureGateway}}
* {{site.data.keyword.contdelivery_full}}

**Etapa 1: armazenar dados na nuvem**
* O {{site.data.keyword.cos_full_notm}} fornece armazenamento de dados históricos, acessível para todos na nuvem pública.
* Use o {{site.data.keyword.cloudant}} com chaves fornecidas pelo desenvolvedor para armazenar dados em cache na nuvem.
* Use o IBM {{site.data.keyword.SecureGateway}} para manter conexões seguras com bancos de dados locais existentes.

**Etapa 2: fornecer acesso a dados com APIs**
* Use o {{site.data.keyword.apiconnect_long}} para a plataforma de economia da API. As APIs permitem que os setores público e privado combinem dados em seus apps.
* Crie clusters para apps públicos/privados, que são conduzidos pelas APIs.
* Estruture apps em um conjunto de microsserviços cooperativos que são executados no Red Hat OpenShift on IBM Cloud, que é baseado em áreas funcionais de apps e suas dependências.
* Implemente os apps em contêineres que são executados no Red Hat OpenShift on IBM Cloud. As ferramentas de HA integradas no Red Hat OpenShift on IBM Cloud equilibram as cargas de trabalho, incluindo a capacidade de recuperação automática e o balanceamento de carga.
* Forneça painéis padronizados do DevOps por meio do Kubernetes, ferramentas de software livre familiares a todos os tipos de Desenvolvedores.

**Etapa 3: inovar com o IBM Garage e os serviços de nuvem**
* Adote as práticas de desenvolvimento agile e iterativa por meio do IBM Garage Method para permitir liberações frequentes de recursos, correções e correções sem tempo de inatividade.
* Se os desenvolvedores estão no setor público ou privado, o {{site.data.keyword.contdelivery_full}} os ajuda a provisionar rapidamente uma cadeia de ferramentas integrada, usando modelos customizáveis e compartilháveis.
* Depois que os Desenvolvedores constroem e testam os apps em seus clusters de Desenvolvimento e Teste, eles usam as cadeias de ferramentas do {{site.data.keyword.contdelivery_full}} para implementar apps em clusters de produção.
* Com o Watson AI, o aprendizado de máquina e as ferramentas de deep learning disponíveis no catálogo do {{site.data.keyword.cloud_notm}}, os Desenvolvedores se concentram em problemas de domínio. Em vez de código ML customizado exclusivo, a lógica de ML é quebrada em apps com ligações de serviços.

** Resultados **
* As parcerias público-privadas normalmente lentas agora aceleram rapidamente os apps em semanas em vez de meses. Essas parcerias de desenvolvimento agora entregam recursos e correções de bug até 10 vezes por semana.
* O desenvolvimento é acelerado quando todos os participantes usam ferramentas de software livre conhecidas, como o Kubernetes. As curvas de aprendizado longo não são mais um bloqueador.
* A transparência das atividades, das informações e dos planos é fornecida aos cidadãos e ao setor privado. Além disso, os cidadãos são integrados a processos governamentais, serviços e suporte.
* As parcerias público-privadas dominam tarefas hercúleas, como o rastreamento de vírus da Zika, a distribuição de eletricidade inteligente, a análise de estatísticas de crime e educação "new collar" universitária.

## A porta pública grande assegura a troca de dados da porta e os manifests de remessa que conectam organizações públicas e privadas
{: #uc_port}

Os Execs de TI para uma companhia de navegação privada e o porto operado pelo governo precisam se conectar, fornecer visibilidade e trocar informações do porto de forma segura. Mas nenhum sistema unificado existia para conectar informações públicas do porto e manifests de remessa privada.
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: o Red Hat OpenShift on IBM Cloud permite que o governo e as parcerias públicas usem serviços de nuvem externos e ferramentas de software livre de fácil colaboração. Os contêineres forneceram uma plataforma compartilhável em que o porto e a companhia de navegação se sentiram seguros de que as informações compartilhadas foram hospedadas em uma plataforma segura. E essa plataforma escala à medida que eles passaram de sistemas pequenos de Desenvolvimento-Teste para sistemas de tamanho de produção. As cadeias de ferramentas abertas aceleraram ainda mais o desenvolvimento, automatizando a construção, o teste e as implementações.

Tecnologias chave:    
* [Clusters que se ajustam às necessidades variadas de CPU, RAM e armazenamento](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [ Segurança do contêiner e isolamento ](/docs/containers?topic=containers-security#security)
* [Ferramentas nativas do DevOps, incluindo cadeias de ferramentas abertas no {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [SDK for Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)

**Contexto: o porto assegura a troca de dados do porto e os manifests de remessa que conectam organizações públicas e privadas.**

* Os grupos distintos de Desenvolvedores do governo e da companhia de navegação não têm uma plataforma unificada na qual eles podem colaborar, o que desacelera as implementações de atualizações e recursos.
* Os desenvolvedores são difundidos no mundo inteiro e ao longo de limites organizacionais, o que significa que o software livre e o PaaS são a melhor opção.
* A segurança é uma preocupação primária e essa preocupação aumenta a carga de colaboração que afeta recursos e atualizações para o software, especialmente após os apps estarem em produção.
* Dados no momento exato significam que os sistemas mundiais devem estar altamente disponíveis para reduzir atrasos em operações de trânsito. Os cronogramas para terminais de remessa são altamente controladas e, em alguns casos, inflexíveis. O uso da web está aumentando, portanto, a instabilidade pode causar experiência do usuário insatisfatória.

** A Solução **

O porto e a companhia de navegação desenvolvem em conjunto um sistema de negociação unificado para enviar eletronicamente informações relacionadas à conformidade para a liberação de mercadorias e navios uma vez, em vez de múltiplas agências. Os apps de manifest e de alfândega podem compartilhar rapidamente os conteúdos de uma remessa específica e assegurar que todos os documentos sejam transferidos e processados eletronicamente por agências para o porto.

Então eles criam uma parceria que é dedicada a soluções para o sistema de comércio:
* DECLARAÇÕES - o app para receber manifests de remessa e processar digitalmente a documentação típica de alfândega e para sinalizar itens fora da política para investigação e cumprimento
* TARIFAS - o app para calcular tarifas, enviar encargos eletronicamente para a transportadora e receber pagamentos digitais
* REGULAMENTAÇÕES - app flexível e configurável que alimenta dois apps anteriores com políticas e regulamentações em constante mudança que afetam importações, exportações e processamento de tarifas

Os desenvolvedores começaram implementando seus apps em contêineres com o Red Hat OpenShift on IBM Cloud. Eles criaram clusters para um ambiente de Desenvolvimento compartilhado que permitem que os Desenvolvedores em todo o mundo implementem de forma colaborativa melhorias de app rapidamente. Os contêineres permitem que cada equipe de desenvolvimento use o idioma de sua escolha.

Segurança primeiro: os IT Execs escolhem os clusters bare metal. Com o bare metal para o Red Hat OpenShift on IBM Cloud, as cargas de trabalho de alfândega sensíveis agora têm um isolamento familiar, mas dentro da flexibilidade da nuvem pública.

Como a empresa de remessa também deseja trabalhar com outras portas, a segurança do app é crucial. Os manifests de remessa e as informações de alfândega são altamente confidenciais. Por meio desse núcleo seguro, o Vulnerability Advisor fornece estas varreduras:
* Varreduras de vulnerabilidades de imagem
* Varreduras de política que são baseadas no ISO 27k
* Varreduras de contêiner ativo
* Varreduras de pacotes para malware conhecido

Ao mesmo tempo, o {{site.data.keyword.iamlong}} ajuda a controlar quem tem qual nível de acesso aos recursos.

Os desenvolvedores se concentram em problemas de domínio, usando ferramentas existentes: em vez de Desenvolvedores que gravam o código exclusivo de criação de log e de monitoramento, eles as encaixam em apps, ligando os serviços do {{site.data.keyword.cloud_notm}} a clusters. Os desenvolvedores também são liberados das tarefas de gerenciamento de infraestrutura porque a IBM cuida do Kubernetes e de upgrades de infraestrutura, segurança e muito mais.

** Modelo de Solução **

Kits do iniciador de cálculo, armazenamento e nó sob demanda que são executados na nuvem pública com acesso seguro aos dados de remessa no mundo inteiro, conforme necessário. O cálculo em clusters é à prova de violação e isolado para o bare metal.  

Solução Técnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.openwhisk}}
* {{site.data.keyword.cloudant}}
* IBM  {{site.data.keyword.SecureGateway}}

**Etapa 1: conteinerizar apps usando microsserviços**
* Use o kit do iniciador Node.js da IBM para iniciar o desenvolvimento.
* Estruture apps em um conjunto de microsserviços cooperativos que são executados no Red Hat OpenShift on IBM Cloud com base em áreas funcionais do app e suas dependências.
* Implemente os apps manifest e de remessa no contêiner que é executado no Red Hat OpenShift on IBM Cloud.
* Forneça painéis padronizados do DevOps por meio do Kubernetes.
* Use o IBM {{site.data.keyword.SecureGateway}} para manter conexões seguras com bancos de dados locais existentes.

** Etapa 2: assegure-se de disponibilidade global **
* Após os Desenvolvedores implementarem os apps em seus clusters de Desenvolvimento e Teste, eles usam as cadeias de ferramentas do {{site.data.keyword.contdelivery_full}} e o Helm para implementar apps específicos do país em clusters no mundo inteiro.
* As cargas de trabalho e os dados podem, então, atender às regulamentações regionais.
* As ferramentas de HA integradas no Red Hat OpenShift on IBM Cloud equilibram a carga de trabalho dentro de cada região geográfica, incluindo a capacidade de recuperação automática e o balanceamento de carga.

** Etapa 3: Compartilhamento de dados **
* {{site.data.keyword.cloudant}} é um banco de dados NoSQL moderno adequado a uma gama de casos de uso acionados por dados, desde o valor de chave até o armazenamento e a consulta de dados complexos orientados a documentos.
* Para minimizar consultas nos bancos de dados regionais, o {{site.data.keyword.cloudant}} é usado para armazenar em cache os dados de sessão do usuário nos apps.
* Essa configuração melhora a usabilidade e o desempenho do aplicativo de front-end em apps no {{site.data.keyword.containershort}}.
* Enquanto os apps do trabalhador no Red Hat OpenShift on IBM Cloud analisam dados no local e armazenam resultados no {{site.data.keyword.cloudant}}, o {{site.data.keyword.openwhisk}} reage a mudanças e limpa automaticamente os dados nos feeds de dados recebidos.
* Da mesma forma, as notificações de remessas em uma região podem ser acionadas por meio de uploads de dados para que todos os consumidores de recebimento de dados possam acessar novos dados.

** Resultados **
* Com os kits do iniciador, o Red Hat OpenShift on IBM Cloud e as ferramentas do {{site.data.keyword.contdelivery_full}}, os Desenvolvedores globais trabalham juntos nas organizações e governos. Eles desenvolvem colaborativamente os apps de alfândega, com ferramentas familiares e interoperáveis.
* Os microsserviços reduzem muito o tempo de entrega de correções, correções de bug e novos recursos. O desenvolvimento inicial é rápido e as atualizações são frequentemente 10 vezes por semana.
* Os clientes de remessa e os oficiais do governo têm acesso a dados de manifest e podem compartilhar dados de alfândega, enquanto obedecem às regulamentações locais.
* A companhia de navegação se beneficia de um melhor gerenciamento de logística na cadeia de suprimento: custos reduzidos e tempos de liberação mais rápidos.
* 99% são declarações digitais e 90% das importações processadas sem intervenção humana.


