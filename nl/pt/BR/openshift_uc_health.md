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

# Os casos de uso do Healthcare para  {{site.data.keyword.cloud_notm}}
{: #cs_uc_health}

Esses casos de uso destacam como as cargas de trabalho no {{site.data.keyword.openshiftlong}} se beneficiam da nuvem pública. Eles têm cálculo seguro sobre bare metal isolado, aceleração fácil de clusters para desenvolvimento mais rápido, migração de máquinas virtuais e compartilhamento de dados em bancos de dados em nuvem.
{: shortdesc}


## O provedor de assistência médica migra cargas de trabalho de VMs ineficientes para contêineres amigáveis para Operações para sistemas de relatório e pacientes
{: #uc_migrate}

Um Exec de TI para um provedor de assistência médica tem relatório de negócios e sistemas de pacientes no local. Esses sistemas passam por ciclos de aprimoramento lento, o que leva a níveis de serviço de pacientes estagnados. 
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: para melhorar o serviço do paciente, o provedor recorreu ao Red Hat OpenShift on IBM Cloud e ao {{site.data.keyword.contdelivery_full}} para reduzir as despesas de TI e acelerar o desenvolvimento, tudo em uma plataforma segura. Os sistemas SaaS de alto uso do provedor, que mantiveram os sistemas de registro de pacientes e apps de relatório de negócios, precisavam de atualizações frequentemente.  No entanto, os desenvolvedores do provedor estavam sobrecarregados com a administração de hardware, rede e até mesmo da pilha do Kubernetes em si. O provedor também queria combater o aumento dos custos de mão de obra e um orçamento decrescente.

Tecnologias chave:
* [Clusters que se ajustam às necessidades variadas de CPU, RAM e armazenamento](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [ Escalação Horizontal ](/docs/containers?topic=containers-app#highly_available_apps)
* [ Segurança do contêiner e isolamento ](/docs/containers?topic=containers-security#security) 
* [{{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/products/cloud-pak-for-data)
* [Ferramentas nativas do DevOps, incluindo cadeias de ferramentas abertas no {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [SDK for Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)
* [Recurso de conexão sem mudar o código do app usando o {{site.data.keyword.appid_short_notm}}](/docs/services/appid?topic=appid-getting-started)

Eles começaram conteinerizando seus sistemas SaaS e colocando-os na nuvem. Nessa primeira etapa, eles foram de hardware superconstruído em um data center privado para cálculo customizável que reduz as operações de TI, a manutenção e a energia. Para hospedar os aplicativos SaaS, eles projetam facilmente os clusters Kubernetes para ajustar suas necessidades de CPU, RAM e armazenamento. Eles usaram o {{site.data.keyword.icp4dfull_notm}} para fornecer as ferramentas de análise de dados familiares por meio de seu ambiente no local. Outro fator para diminuir os custos de equipe é que a IBM gerencia o Kubernetes, para que o provedor possa se concentrar em entregar o melhor atendimento ao cliente. 

O desenvolvimento acelerado é a vitória chave para o Exec de TI. Com a mudança para a nuvem pública, os Desenvolvedores podem experimentar facilmente com o SDK do Node.js, enviando por push as mudanças para os sistemas de Desenvolvimento e Teste, escalados em clusters separados. Esses pushes foram automatizados com cadeias de ferramentas abertas e o {{site.data.keyword.contdelivery_full}}. As atualizações para o sistema SaaS não mais se arrastam em processos de construção lentos e propensos a erros. Os Desenvolvedores podem fornecer atualizações incrementais para seus usuários, diariamente ou ainda mais frequentemente.  Além disso, a criação de log e o monitoramento para os sistemas SaaS, especialmente como os relatórios de front-end e backend de paciente interagem, se integram rapidamente ao sistema. Os desenvolvedores não perdem tempo construindo sistemas de criação de log complexos, apenas para solucionar problemas de sistemas em tempo real.

Segurança primeiro: com o bare metal para o Red Hat OpenShift on IBM Cloud, as cargas de trabalho sensíveis de pacientes agora têm um isolamento familiar, mas dentro da flexibilidade da nuvem pública. Nesse núcleo, o Vulnerability Advisor fornece varredura:
* Varredura de Vulnerabilidade de Imag
* Varredura de política com base no ISO 27k
* Varredura de contêiner ativo
* Varredura de pacote para malware conhecido

Os dados seguros do paciente levam a pacientes mais felizes.

**Contexto: migração de carga de trabalho para o Provedor de assistência médica**

* A dívida técnica, que é acoplada a ciclos de liberação longos, está prejudicando os sistemas de gerenciamento e relatório do paciente de negócios críticos do provedor.
* Seus aplicativos customizados de funções administrativas de apoio e de atendimento são entregues no local, em imagens de máquina virtual monolíticas.
* Eles precisam revisar seus processos, métodos e ferramentas, mas não sabem muito bem por onde começar.
* Sua dívida técnica está crescendo, não reduzindo, com a incapacidade de liberar o software de qualidade para acompanhar as demandas de mercado.
* A segurança é uma preocupação primária e esse problema está somando-se à carga de entrega, que causa ainda mais atrasos.
* Os orçamentos de despesa de capital estão sob controle apertado e o TI acha que eles não têm o orçamento ou a equipe para criar as paisagens de teste e de preparação necessárias com seus sistemas internos.

** Modelo de Solução **

Os serviços de cálculo, de armazenamento e de E/S on demand são executados na nuvem pública com acesso seguro aos ativos corporativos no local. Implemente um processo CI/CD e outras partes do IBM Garage Method para encurtar dramaticamente os ciclos de entrega.

** Etapa 1: Proteger a plataforma de cálculo **
* Por meio desse núcleo, o Vulnerability Advisor fornece varredura de vulnerabilidade de varredura de imagem, política, contêiner e empacotamento, para malware conhecido.
* Cumpra consistentemente a autenticação acionada por política para seus serviços e APIs com uma anotação simples de Ingress. Com a segurança declarativa, é possível assegurar a autenticação do usuário e a validação do token usando o {{site.data.keyword.appid_short_notm}}.

** Etapa 2: Levantar e deslocar **
* Migre as imagens de máquina virtual para imagens de contêiner que são executadas no Red Hat OpenShift on IBM Cloud na nuvem pública.
* Implemente o {{site.data.keyword.icp4dfull_notm}}, para que os desenvolvedores tenham suas ferramentas de análise de dados familiares na nuvem.
* Forneça painéis e práticas padronizados do DevOps por meio do Kubernetes.
* Ative o ajuste de escala sob demanda de cálculo para lote e outras cargas de trabalho de funções administrativas de apoio que são executadas com pouca frequência.
* Use o {{site.data.keyword.SecureGatewayfull}} para manter conexões seguras com o DBMS no local.
* O data center privado/os custos de capital no local são bastante reduzidos e substituídos por um modelo de computação utilitária que é escalado com base na demanda de carga de trabalho.

** Etapa 3: Microserviços e Método de Garagem **
* Reprojete apps em um conjunto de microsserviços cooperativos. Esse conjunto é executado dentro do Red Hat OpenShift on IBM Cloud que é baseado em áreas funcionais do app com a maioria dos problemas de qualidade.
* Use o {{site.data.keyword.cloudant}} com chaves fornecidas pelo cliente para armazenar dados em cache na nuvem.
* Adote as práticas de integração e entrega contínuas (CI/CD) para que os Desenvolvedores criem versão e liberem um microsserviço em seu próprio planejamento, conforme necessário. O {{site.data.keyword.contdelivery_full}} fornece cadeias de ferramentas de fluxo de trabalho para o processo CI/CD juntamente com a criação de imagem e a varredura de vulnerabilidade de imagens de contêiner.
* Adote as práticas de desenvolvimento agile e iterativo do IBM Garage Method para permitir liberações frequentes de novas funções, correções e correções sem tempo de inatividade.

** Solução Técnica **
* Red Hat OpenShift on IBM Cloud 
* {{site.data.keyword.icp4dfull_notm}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.SecureGatewayfull}}
* {{site.data.keyword.appid_short_notm}}

Para as cargas de trabalho mais sensíveis, os clusters podem ser hospedados no Red Hat OpenShift on IBM Cloud for Bare Metal. Usando a tecnologia de contêineres padrão de mercado, inicialmente os apps podem ser hospedados novamente no Red Hat OpenShift on IBM Cloud rapidamente sem grandes mudanças arquiteturais. Essa mudança fornece o benefício imediato de escalabilidade.

Eles podem replicar e escalar os apps usando regras definidas e o orquestrador do Kubernetes automatizado. O Red Hat OpenShift on IBM Cloud fornece recursos de cálculo escaláveis e os painéis do DevOps associados para criar, escalar e derrubar apps e serviços on demand. Usando os objetos de implementação e de tempo de execução do Kubernetes, o provedor pode monitorar e gerenciar upgrades para apps de forma confiável.

O {{site.data.keyword.SecureGatewayfull}} é usado para criar um pipeline seguro para bancos de dados no local e documentos para apps que são hospedados novamente para execução no Red Hat OpenShift on IBM Cloud.

{{site.data.keyword.cloudant}} é um banco de dados NoSQL moderno adequado a uma gama de casos de uso acionados por dados, desde o valor de chave até o armazenamento e a consulta de dados complexos orientados a documentos. Para minimizar as consultas para o RDBMS de funções administrativas de apoio, o {{site.data.keyword.cloudant}} é usado para armazenar em cache os dados da sessão do usuário entre os apps. Essas opções melhoram a usabilidade e o desempenho do app front-end entre os apps no Red Hat OpenShift on IBM Cloud.

Mover as cargas de trabalho de cálculo para o {{site.data.keyword.cloud_notm}} não é o suficiente. O provedor precisa passar por uma transformação de processo e métodos também. Adotando as práticas do IBM Garage Method, o provedor pode implementar um processo de entrega agile e iterativo que suporta práticas modernas do DevOps como CI/CD.

Grande parte do processo CI/CD propriamente dito é automatizado com o serviço de Entrega Contínua da IBM no Cloud. O provedor pode definir cadeias de ferramentas de fluxo de trabalho para preparar imagens de contêiner, verificar vulnerabilidades e implementá-las no cluster do Kubernetes.

** Resultados **
* Levantar as VMs monolíticas existentes em contêineres hospedados em nuvem foi uma primeira etapa que permitiu ao provedor economizar em custos de capital e iniciar o aprendizado de práticas modernas do DevOps. 
* Com o Cloud Pak implementado, o provedor transferia o suporte de pilha integral de suas ferramentas de análise de dados para a IBM, até mesmo o gerenciamento de ciclo de vida dessas ferramentas. Seus desenvolvedores ficavam aliviados das tarefas de operações e podiam focar em novos recursos e atualizações. 
* A rearquitetura de aplicativos monolíticos chave para um conjunto de microsserviços de baixa granularidade reduziu o tempo de entrega de correções, correções de bug e novos recursos.
* Em paralelo, o provedor implementou iterações de prazo fechado simples para obter um identificador na dívida técnica existente.

## A pesquisa sem fins lucrativos hospeda com segurança os dados sensíveis enquanto aumenta a pesquisa com parceiros
{: #uc_research}

Um Exec de Desenvolvimento para uma pesquisa de doença sem fins lucrativos tem pesquisadores acadêmicos e industriais que não podem compartilhar dados de pesquisa facilmente. Em vez disso, o trabalho deles é isolado em áreas no mundo inteiro devido às regulamentações regionais de conformidade e bancos de dados centralizados.
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: o Red Hat OpenShift on IBM Cloud fornece cálculo seguro que pode hospedar o processamento de dados sensíveis e de desempenho em uma plataforma aberta. Essa plataforma global é hospedada em regiões próximas. Portanto, ela está vinculada às regulamentações locais que inspiram a confiança dos pacientes e dos pesquisadores de que seus dados são protegidos localmente e que fazem a diferença em melhores resultados de saúde.

Tecnologias chave:
* [ O planejamento inteligente coloca cargas de trabalho onde necessário ](/docs/containers?topic=containers-regions-and-zones#regions-and-zones)
* [{{site.data.keyword.cloudant}} para persistir e sincronizar dados entre os apps](/docs/services/Cloudant?topic=cloudant-getting-started#getting-started)
* [Varredura de vulnerabilidade e isolamento para cargas de trabalho](/docs/services/Registry?topic=va-va_index#va_index)
* [Ferramentas nativas do DevOps, incluindo cadeias de ferramentas abertas no {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [{{site.data.keyword.openwhisk}} para limpar os dados e notificar pesquisadores sobre mudanças de estrutura de dados](/docs/openwhisk?topic=cloud-functions-pkg_cloudant#openwhisk_cloudant)

**Contexto: hospedando e compartilhando com segurança dados de doença para Pesquisa sem fins lucrativos**

* Grupos distintos de pesquisadores de várias instituições não têm uma forma unificada de compartilhar dados, reduzindo a colaboração.
* A preocupação com a segurança soma-se à carga de colaboração, que dá origem a ainda menos pesquisa compartilhada.
* Os Desenvolvedores e os Pesquisadores são difundidos no mundo inteiro e ao longo de limites organizacionais, que tornam o PaaS e o SaaS a melhor opção para cada grupo de usuários.
* As diferenças regionais em regulamentações de saúde requerem que alguns dados e processamento de dados permaneçam dentro dessa região.

** A Solução **

A pesquisa sem fins lucrativos deseja agregar dados de pesquisa do câncer em todo o mundo. Então eles criam uma divisão que é dedicada a soluções para seus pesquisadores:
* ALIMENTAR - apps para alimentar dados de pesquisa. Hoje em dia, os pesquisadores usam planilhas, documentos, produtos comerciais e bancos de dados proprietários ou internos para registrar resultados de pesquisa. É improvável que essa situação mude com a tentativa sem fins lucrativos de centralizar a análise de dados.
* ANONIMAR - apps para anonimar os dados. O SPI deve ser removido para obedecer às regulamentações de saúde regionais.
* ANALISAR - apps para analisar os dados. O padrão básico é armazenar os dados em um formato regular e, em seguida, consultar e processá-los usando tecnologia de AI e aprendizado de máquina (ML), regressões simples e assim por diante.

Os pesquisadores precisam se afiliar a um cluster regional e os apps alimentam, transformam e anonimam os dados:
1. Sincronizando os dados anonimados em clusters regionais ou enviando-os para um armazenamento de dados centralizado
2. Processando os dados, usando ML como PyTorch em nós do trabalhador bare metal que fornecem GPUs

**ALIMENTAR** O {{site.data.keyword.cloudant}} é usado em cada cluster regional que armazena os documentos de dados ricos dos pesquisadores e pode ser consultado e processado conforme necessário. O {{site.data.keyword.cloudant}} criptografa dados em repouso e em trânsito, que obedecem às leis regionais de privacidade de dados.

O {{site.data.keyword.openwhisk}} é usado para criar funções de processamento que alimentam dados de pesquisa e os armazenam como documentos de dados estruturados no {{site.data.keyword.cloudant}}. O {{site.data.keyword.SecureGatewayfull}} fornece uma maneira fácil para o {{site.data.keyword.openwhisk}} acessar os dados no local de uma maneira segura.

Os apps da web nos clusters regionais são desenvolvidos em nodeJS para a entrada de dados manuais de resultados, definição de esquema e afiliação de organizações de pesquisa. O IBM Key Protect ajuda a proteger o acesso aos dados do {{site.data.keyword.cloudant}} e o IBM Vulnerability Advisor varre contêineres de app e imagens para explorações de segurança.

**ANONIMAR** Sempre que um novo documento de dados é armazenado no {{site.data.keyword.cloudant}}, um evento é acionado e uma Função de nuvem anonima os dados e remove o SPI do documento de dados. Esses documentos de dados anonimados são armazenados separados dos dados "brutos" que são alimentados e são os únicos documentos compartilhados entre regiões para análise.

**ANALISAR** As estruturas de aprendizado de máquina são altamente intensivas em cálculo e, portanto, aquelas sem fins lucrativos configuram um cluster de processamento global de nós do trabalhador bare metal. Associado a esse cluster de processamento global está um banco de dados {{site.data.keyword.cloudant}} agregado dos dados anonimados. Uma tarefa cron aciona periodicamente uma Função de nuvem para enviar por push documentos de dados anonimados dos centros regionais para a instância do {{site.data.keyword.cloudant}} do cluster de processamento global.

O cluster de cálculo executa a estrutura de PyTorch ML e os apps de aprendizado de máquina são gravados em Python para analisar os dados agregados. Além dos apps ML, os pesquisadores no grupo coletivo também desenvolvem seus próprios apps que podem ser publicados e executados no cluster global.

A organização sem fins lucrativos também fornece apps que são executados em nós não bare metal do cluster global. Os apps visualizam e extraem os dados agregados e a saída de app ML. Esses apps são acessíveis por um terminal público, que é protegido pelo Gateway da API para o mundo. Em seguida, os pesquisadores e analistas de dados de todos os lugares podem fazer download de conjuntos de dados e fazer sua própria análise.

**Hospedando cargas de trabalho de pesquisa no Red Hat OpenShift on IBM Cloud**

Os desenvolvedores começaram implementando seus apps SaaS de compartilhamento de pesquisa em contêineres com o Red Hat OpenShift on IBM Cloud. Eles criaram clusters para um ambiente de Desenvolvimento que permitem que os Desenvolvedores no mundo inteiro implementem colaborativamente melhorias de app de forma rápida.

Segurança primeiro: o Development Exec escolheu o bare metal para hospedar os clusters de pesquisa. Com o bare metal para o Red Hat OpenShift on IBM Cloud, as cargas de trabalho de pesquisa sensíveis agora têm um isolamento familiar, mas dentro da flexibilidade da nuvem pública. Como essa organização sem fins lucrativos também tem uma parceria com as empresas farmacêuticas, a segurança do app é crucial. A competição é acirrada e a espionagem corporativa é possível. Nesse núcleo seguro, o Vulnerability Advisor fornece varredura:
* Varredura de Vulnerabilidade de Imag
* Varredura de política com base no ISO 27k
* Varredura de contêiner ativo
* Varredura de pacote para malware conhecido

Os apps de pesquisa protegidos levam ao aumento da participação de avaliação clínica.

Para alcançar a disponibilidade global, os sistemas de Desenvolvimento, Teste e Produção são implementados no mundo inteiro em vários data centers. Para HA, eles usam uma combinação de clusters em múltiplas regiões geográficas, bem como clusters de múltiplas zonas. Eles podem implementar facilmente o app de pesquisa em clusters de Frankfurt para conformidade com a regulamentação europeia local. Eles também implementam o app dentro dos clusters dos Estados Unidos para assegurar a disponibilidade e a recuperação localmente. Eles também difundem a carga de trabalho de pesquisa em clusters de várias zonas em Frankfurt para assegurar que o app europeu esteja disponível e também equilibre a carga de trabalho de forma eficiente. Como os pesquisadores estão fazendo upload de dados sensíveis com o app de compartilhamento de pesquisa, os clusters do app são hospedados em regiões onde regulamentações mais restritas se aplicam.

Os desenvolvedores se concentram em problemas de domínio, usando as ferramentas existentes: em vez de gravar o código ML exclusivo, a lógica ML é encaixada em apps, ligando os serviços do {{site.data.keyword.cloud_notm}} aos clusters. Os desenvolvedores também são liberados das tarefas de gerenciamento de infraestrutura porque a IBM cuida do Kubernetes e de upgrades de infraestrutura, segurança e muito mais.

** A Solução **

Os kits do iniciador de cálculo, armazenamento e nó sob demanda são executados em nuvem pública com acesso seguro a dados de pesquisa no mundo inteiro, conforme garantido. O cálculo em clusters é à prova de violação e isolado para o bare metal.

Solução Técnica:
* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.openwhisk}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.SecureGatewayfull}}

**Etapa 1: conteinerizar apps usando microsserviços**
* Use o kit iniciador do Node.js da IBM para iniciar o desenvolvimento.
* Estruture os apps em um conjunto de microsserviços cooperativos dentro do Red Hat OpenShift on IBM Cloud com base nas áreas funcionais do app e suas dependências.
* Implemente os apps de pesquisa em contêineres no Red Hat OpenShift on IBM Cloud.
* Forneça painéis padronizados do DevOps por meio do Kubernetes.
* Ative o ajuste de escala sob demanda de cálculo para lote e outras cargas de trabalho de pesquisa que são executadas com pouca frequência.
* Use o {{site.data.keyword.SecureGatewayfull}} para manter as conexões seguras com os bancos de dados no local existentes.

** Etapa 2: usar cálculo seguro e de desempenho**
* Os apps ML que requerem um cálculo de desempenho mais alto são hospedados no Red Hat OpenShift on IBM Cloud no Bare Metal. Esse cluster ML é centralizado, portanto, cada cluster regional não tem a despesa de trabalhadores de bare metal; as implementações do Kubernetes são mais fáceis também.
* O Vulnerability Advisor fornece imagem, política, contêiner e varredura de vulnerabilidade de pacote para malware conhecido.

** Etapa 3: assegure-se de disponibilidade global **
* Depois que os Desenvolvedores constroem e testam os apps em seus clusters de Desenvolvimento e teste, eles usam as cadeias de ferramentas CI/CD da IBM para implementar apps nos clusters em todo o globo.
* As ferramentas de HA integradas no Red Hat OpenShift on IBM Cloud equilibram a carga de trabalho dentro de cada região geográfica, incluindo a capacidade de recuperação automática e o balanceamento de carga.
* Com as cadeias de ferramentas e ferramentas de implementação do Helm, os apps também são implementados em clusters no mundo inteiro, portanto, as cargas de trabalho e os dados atendem às regulamentações regionais.

** Etapa 4: Compartilhamento de dados **
* {{site.data.keyword.cloudant}} é um banco de dados NoSQL moderno adequado a uma gama de casos de uso acionados por dados, desde o valor de chave até o armazenamento e a consulta de dados complexos orientados a documentos.
* Para minimizar consultas nos bancos de dados regionais, o {{site.data.keyword.cloudant}} é usado para armazenar em cache os dados de sessão do usuário nos apps.
* Essa opção melhora a usabilidade e o desempenho do app front-end entre os apps no Red Hat OpenShift on IBM Cloud.
* Enquanto os apps do trabalhador no Red Hat OpenShift on IBM Cloud analisam dados no local e armazenam resultados no {{site.data.keyword.cloudant}}, o {{site.data.keyword.openwhisk}} reage a mudanças e limpa automaticamente os dados nos feeds de dados recebidos.
* Da mesma forma, as notificações de avanços de pesquisa em uma região podem ser acionadas por meio de uploads de dados para que todos os pesquisadores possam tirar vantagem dos novos dados.

** Resultados **
* Com kits do iniciador, o Red Hat OpenShift on IBM Cloud e as ferramentas IBM CI/CD, os desenvolvedores globais funcionam em instituições e desenvolvem apps de pesquisa de forma colaborativa, com ferramentas familiares e interoperáveis.
* Os microsserviços reduzem muito o tempo de entrega de correções, correções de bug e novos recursos. O desenvolvimento inicial é rápido e as atualizações são frequentes.
* Os pesquisadores têm acesso a dados clínicos e podem compartilhar dados clínicos, enquanto eles obedecem às regulamentações locais.
* Os pacientes que participam da pesquisa de doenças se sentem confiantes de que seus dados estão seguros e fazendo a diferença, quando são compartilhados com grandes equipes de pesquisa.


