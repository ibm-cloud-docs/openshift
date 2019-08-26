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

# Casos de uso de serviços financeiros para  {{site.data.keyword.cloud_notm}}
{: #cs_uc_finance}

Esses casos de uso destacam como as cargas de trabalho no {{site.data.keyword.openshiftlong}} podem
aproveitar a alta disponibilidade, o cálculo de alto desempenho,
a aceleração fácil de clusters para desenvolvimento mais rápido e AI do {{site.data.keyword.ibmwatson}}.
{: shortdesc}

## A empresa de hipoteca reduz os custos e acelera a conformidade regulamentar
{: #uc_mortgage}

Um VP de Gerenciamento de Risco para uma empresa de hipoteca residencial processa 70 milhões de registros por dia, mas o sistema no local estava lento e também inexato. As despesas de TI subiram porque o hardware ficou desatualizado rapidamente e não foi totalmente utilizado. Enquanto aguardavam o fornecimento de hardware, sua conformidade regulamentar desacelerou. 
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: para melhorar a análise de risco, a empresa recorreu aos serviços do Red Hat OpenShift on IBM Cloud e do IBM Cloud Analytic para reduzir custos, aumentar a disponibilidade mundial e, em última instância, acelerar a conformidade regulamentar. Com o Red Hat OpenShift on IBM Cloud em múltiplas regiões, seus apps de análise podem ser conteinerizados e implementados no mundo, melhorando a disponibilidade e abordando regulamentos locais. Essas implementações são aceleradas com ferramentas de software livre familiares, já parte do Red Hat OpenShift on IBM Cloud.

Red Hat OpenShift on IBM Cloud e principais tecnologias:
* [ Escalação Horizontal ](/docs/containers?topic=containers-app#highly_available_apps)
* [ Diversas regiões para alta disponibilidade ](/docs/containers?topic=containers-regions-and-zones#regions-and-zones)
* [Clusters que se ajustam às necessidades variadas de CPU, RAM e armazenamento](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [ Segurança do contêiner e isolamento ](/docs/containers?topic=containers-security#security)
* [{{site.data.keyword.cloudant}} para persistir e sincronizar dados entre os apps](/docs/services/Cloudant?topic=cloudant-getting-started#getting-started)
* [SDK for Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)

** A Solução **

Eles iniciaram conteinerizando os apps de análise e colocando-os na nuvem. Em um piscar de olhos, suas dores de cabeça de hardware foram embora. Eles foram capazes de projetar facilmente os clusters do Kubernetes para ajustar sua CPU de alto desempenho, RAM, armazenamento e necessidades de segurança. E quando os apps de análise deles mudam, eles podem incluir ou reduzir cálculo sem grandes investimentos de hardware. Com a escala horizontal do Red Hat OpenShift on IBM Cloud, seus apps escalam com o número crescente de registros, resultando em relatórios regulamentares mais rápidos. O Red Hat OpenShift on IBM Cloud fornece recursos de cálculo elásticos em todo o mundo que são seguros e altamente eficientes para o uso integral dos recursos de cálculo modernos.

Agora, esses apps recebem dados de alto volume de um data warehouse no {{site.data.keyword.cloudant}}. O armazenamento baseado em nuvem no {{site.data.keyword.cloudant}} assegura uma disponibilidade mais alta do que quando ele foi bloqueado em um sistema no local. Como a disponibilidade é essencial, os apps são implementados em data centers globais: para DR e para latência também.

Eles também aceleraram sua análise de risco e conformidade. Suas funções de análise preditiva e de risco, como cálculos de Monte Carlo, são agora constantemente atualizadas por meio de implementações agile iterativas. A orquestração de contêiner é manipulada por um Kubernetes gerenciado para que os custos de operações sejam reduzidos também. Por fim, a análise de risco para hipotecas é mais responsiva às rápidas mudanças no mercado.

**Contexto: conformidade e modelagem financeira para hipotecas residenciais**

* A necessidade elevada de melhor gerenciamento de risco financeiro impulsiona aumentos na supervisão regulamentar. As mesmas necessidades impulsionam a revisão associada dos processos de avaliação de risco e a divulgação de relatórios regulamentares mais granulares, integrados e abundantes.
* Os High Performance Computing Grids são os principais componentes de infraestrutura para modelagem financeira.

Nesse momento, o problema da empresa é a escala e o tempo de entrega.

Seu ambiente atual é no local e tem sete anos a mais de idade, com cálculo, armazenamento e capacidade de E/S limitados.
As atualizações do servidor são dispendiosas e levam muito tempo para serem concluídas.
As atualizações de software e app seguem um processo informal e não são repetidas.
A grade HPC real é difícil de ser programada. A API é muito complexa para os novos Desenvolvedores que são trazidos para a equipe e requer conhecimento não documentado.
Além disso, os upgrades de app principais levam de 6 a 9 meses para serem concluídos.

**Modelo de solução: Serviços de computação, armazenamento e E/S on-demand que são executados em nuvem pública com acesso seguro aos recursos corporativos locais conforme necessário**

* Armazenamento de documento seguro e escalável que suporta consulta de documento estruturado e não estruturado
* "Levantar e deslocar" o app e os ativos corporativos existentes enquanto eles ativaram a integração para alguns sistemas no local que não serão migrados
* Reduzir o tempo de implementação das soluções e implementar processos padrão do DevOps e de monitoramento para tratar erros que afetaram a precisão do relatório

** Solução detalhada **

* Red Hat OpenShift on IBM Cloud
* {{site.data.keyword.cos_full_notm}}
* {{site.data.keyword.sqlquery_notm}}  (Spark)
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.SecureGateway}}

O Red Hat OpenShift on IBM Cloud fornece recursos de cálculo escaláveis e os painéis do DevOps associados para criar, escalar e derrubar apps e serviços on demand. Usando contêineres padrão de mercado, os apps podem ser hospedados de novo inicialmente no Red Hat OpenShift on IBM Cloud de forma rápida sem grandes mudanças arquiteturais.

Essa solução fornece o benefício imediato de escalabilidade. Usando o rico conjunto de objetos de implementação e tempo de execução do Kubernetes, a empresa de hipoteca monitora e gerencia os upgrades para apps com confiança. Eles também são capazes de replicar e escalar os apps que usam regras definidas e o orquestrador do Kubernetes automatizado.

O {{site.data.keyword.SecureGateway}} é usado para criar um pipeline seguro para bancos de dados no local e documentos para apps que são hospedados novamente para execução no Red Hat OpenShift on IBM Cloud.

O {{site.data.keyword.cos_full_notm}} é para todo documento bruto e armazenamento de dados à medida que eles avançam. Para simulações de Monte Carlo, é adotado um pipeline de fluxo de trabalho no qual os dados de simulação estão em arquivos estruturados armazenados no {{site.data.keyword.cos_full_notm}}. Um acionador para iniciar a simulação escala serviços de cálculo no Red Hat OpenShift on IBM Cloud para dividir os dados dos arquivos em N depósitos de eventos para processamento de simulação. O Red Hat OpenShift on IBM Cloud é escalado automaticamente para N execuções de serviço associadas e grava resultados intermediários no {{site.data.keyword.cos_full_notm}}. Esses resultados são processados por outro conjunto dos serviços de cálculo do Red Hat OpenShift on IBM Cloud para produzir os resultados finais.

O {{site.data.keyword.cloudant}} é um banco de dados NoSQL moderno que é útil para muitos casos de uso acionados por dados: de key-value a armazenamento de dados e consulta de dados orientados a documentos complexos. Para gerenciar o conjunto crescente de regras de relatório regulamentares e de gerenciamento, a empresa de hipoteca usa o {{site.data.keyword.cloudant}} para armazenar documentos associados a dados regulamentares brutos que são recebidos. Os processos de cálculo no Red Hat OpenShift on IBM Cloud são acionados para compilar, processar e publicar os dados em vários formatos de relatório. Os resultados intermediários comuns entre os relatórios são armazenados como documentos do {{site.data.keyword.cloudant}} para que processos orientados por modelo possam ser usados para produzir os relatórios necessários.

** Resultados **

* As simulações financeiras complexas são concluídas em 25% do tempo do que era possível anteriormente com os sistemas existentes no local.
* O tempo para a implementação melhorou dos 6 - 9 meses anteriores para 1 - 3 semanas em média. Essa melhoria ocorre porque o Red Hat OpenShift on IBM Cloud permite que um processo disciplinado e controlado aumente os contêineres do app e os substitua por versões mais novas. Os erros de relatório podem ser corrigidos rapidamente tratando dos problemas, como precisão.
* Os custos de relatórios regulamentares foram reduzidos com um conjunto consistente e escalável de serviços de armazenamento e cálculo que o Red Hat OpenShift on IBM Cloud e o {{site.data.keyword.cloudant}} trazem.
* Com o tempo, os apps originais que inicialmente eram "levantados e deslocados" para a nuvem foram rearquitetados em microsserviços cooperativos que são executados no Red Hat OpenShift on IBM Cloud. Essa ação acelerou o desenvolvimento e o tempo para implementação e permitiu mais inovação devido à relativa facilidade de experimentação. Eles também liberaram apps inovadores com versões mais recentes de microsserviços para aproveitar as condições de mercado e negócios (ou seja, chamados de apps e microsserviços situacionais).


## A empresa de tecnologia de pagamento aperfeiçoa a produtividade do desenvolvedor, implementando ferramentas ativadas por AI para seus parceiros 4 vezes mais rápido
{: #uc_payment_tech}

Um Exec de desenvolvimento tem Desenvolvedores que usam ferramentas de aplicativo no local que desaceleram a criação de protótipos enquanto aguardam pela compra de hardware.
{: shortdesc}

Por que o {{site.data.keyword.cloud_notm}}: o Red Hat OpenShift on IBM Cloud fornece o spin-up de cálculo usando a tecnologia padrão de software livre. Após a empresa ser movida para o Red Hat OpenShift on IBM Cloud, os Desenvolvedores têm acesso a ferramentas aliadas ao DevOps, como contêineres móveis e facilmente compartilhados.

Em seguida, os Desenvolvedores podem experimentar facilmente, enviando por push mudanças para sistemas de Desenvolvimento e teste rapidamente com cadeias de ferramentas abertas. Suas ferramentas de desenvolvimento de aplicativo ficam com um novo visual quando incluem serviços de nuvem de IA em apps com um clique.

Tecnologias chave:
* [Clusters que se ajustam às necessidades variadas de CPU, RAM e armazenamento](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes)
* [Ferramentas nativas do DevOps, incluindo cadeias de ferramentas abertas no {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [IBM Cloud Pak for Applications](https://www.ibm.com/cloud/cloud-pak-for-applications)
* [ Prevenção de Fraude com  {{site.data.keyword.watson}}  AI ](https://www.ibm.com/cloud/watson-studio)
* [Ferramentas nativas do DevOps, incluindo cadeias de ferramentas abertas no {{site.data.keyword.contdelivery_full}}](https://www.ibm.com/cloud/garage/toolchains/)
* [SDK for Node.js](/docs/runtimes/nodejs?topic=Nodejs-nodejs_runtime#nodejs_runtime)
* [Recurso de conexão sem mudar o código do app usando o {{site.data.keyword.appid_short_notm}}](/docs/services/appid?topic=appid-getting-started)

**Contexto: aperfeiçoando a produtividade do desenvolvedor e implementando ferramentas de AI para parceiros 4 vezes mais rápido**

* A interrupção está desenfreada na indústria de pagamentos que também tem um crescimento dramático nos segmentos de consumidor e entre empresas. Mas as atualizações para as ferramentas de pagamento eram lentas.
* Os recursos cognitivos são necessários para destinar transações fraudulentas de maneiras novas e mais rápidas.
* Com o número crescente de parceiros e suas transações, o tráfego de ferramentas aumenta, mas seu orçamento de infraestrutura precisa diminuir, maximizando a eficiência dos recursos.
* Sua dívida técnica está crescendo, não reduzindo, com a incapacidade de liberar o software de qualidade para acompanhar as demandas de mercado.
* Os orçamentos de despesa de capital estão sob controle apertado e o TI acha que eles não têm o orçamento ou a equipe para criar as paisagens de teste e de preparação com seus sistemas internos.
* A segurança é cada vez mais uma preocupação primária e essa preocupação apenas soma-se à carga de entrega e tudo isso causa ainda mais atrasos.

** A Solução **

O Exec de Desenvolvimento é confrontado com muitos desafios na indústria de pagamento dinâmico. As regulamentações, os comportamentos dos consumidores, a fraude, os concorrentes e as infraestruturas de mercado estão todos se desenvolvendo rapidamente. O desenvolvimento com ritmo rápido é essencial para fazer parte do futuro mundo de pagamentos.

O modelo de negócio deles é fornecer ferramentas de pagamento a parceiros de negócios, para que eles possam ajudar essas instituições financeiras e outras organizações a entregarem experiências de pagamento digital rico em segurança.

Eles precisam de uma solução que ajude os Desenvolvedores e seus parceiros de negócios:
* FRONT-END PARA FERRAMENTAS DE PAGAMENTO: sistemas de taxas, rastreamento de pagamento incluindo internacional, conformidade regulamentar, biometria, remessa e muito mais
* RECURSOS ESPECÍFICOS DA REGULAMENTAÇÃO: cada país tem regulamentações exclusivas para que o conjunto de ferramentas geral possa parecer semelhante, mas mostrar benefícios específicos do país
* FERRAMENTAS FÁCEIS PARA O DESENVOLVEDOR que aceleram a apresentação de recursos e correções de bugs
* O FRAUD DETECTION AS A SERVICE (FDaaS) usa o {{site.data.keyword.watson}} AI para manter-se um passo à frente das frequentes e crescentes ações fraudulentas

** Modelo de Solução **

Cálculo sob demanda, ferramentas do DevOps e AI que são executados na nuvem pública com acesso a sistemas de pagamentos de backend. Implemente um processo CI/CD para encurtar dramaticamente os ciclos de entrega.

Solução Técnica:
* Red Hat OpenShift on IBM Cloud
* IBM Cloud Pak for Applications
* {{site.data.keyword.contdelivery_full}}
* IBM Cloud Logging and Monitoring
* {{site.data.keyword.ibmwatson_notm}}  para Serviços Financeiros
* {{site.data.keyword.appid_full_notm}}

Eles iniciaram por meio da conteinerização das VMs da ferramenta de pagamento e colocando-as na nuvem. Em um piscar de olhos, suas dores de cabeça de hardware foram embora. Eles foram capazes de projetar facilmente os clusters do Kubernetes para ajustar suas necessidades de CPU, RAM, armazenamento e segurança. E quando suas ferramentas de pagamento precisam mudar, elas podem incluir ou reduzir o cálculo sem compras caras e lentas de hardware.

Com a escala horizontal do Red Hat OpenShift on IBM Cloud, seus apps são escalados com o número crescente de parceiros, resultando em um crescimento mais rápido. O Red Hat OpenShift on IBM Cloud fornece recursos de cálculo elásticos em todo o mundo que são seguros para uso integral de recursos de cálculo modernos.

O desenvolvimento acelerado é uma vitória chave para o Exec. Com o uso de contêineres modernos, os Desenvolvedores podem experimentar facilmente nos idiomas de sua escolha, enviar por push as mudanças para os sistemas de Desenvolvimento e Teste, escalados em clusters separados. Esses pushes foram automatizados com cadeias de ferramentas abertas e o {{site.data.keyword.contdelivery_full}}. As atualizações para as ferramentas não mais se arrastam em processos de construção lentos e propensos a erros. Eles podem entregar atualizações incrementais para suas ferramentas, diariamente ou ainda mais frequentemente.

Além disso, a criação de log e o monitoramento para as ferramentas, especialmente onde eles usavam o {{site.data.keyword.watson}} AI, se integram rapidamente ao sistema. Os Desenvolvedores não desperdiçam o tempo construindo sistemas de criação de log complexos, apenas para serem capazes de solucionar problemas de seus sistemas em tempo real. Um fator chave para menos custos de equipe é que a IBM gerencia o Kubernetes, para que os Desenvolvedores possam se concentrar em ferramentas de pagamento melhores.

Segurança primeiro: com o bare metal para o Red Hat OpenShift on IBM Cloud, as ferramentas sensíveis de pagamento agora têm um isolamento familiar, mas dentro da flexibilidade da nuvem pública. As varreduras para vulnerabilidades e malware são executadas continuamente.

**Etapa 1: levantar e deslocar para cálculo seguro**
* Migre imagens de máquina virtual para imagens de contêiner que são executadas no Red Hat OpenShift on IBM Cloud no {{site.data.keyword.Bluemix_notm}} público. Implemente o IBM Cloud Pak for Applications, para que os desenvolvedores tenham suas ferramentas de desenvolvimento de aplicativo familiares na nuvem. 
* Nesse núcleo, o Vulnerability Advisor fornece varredura de vulnerabilidade de imagem, política, contêiner e empacotamento, para malware conhecido.
* O data center privado/os custos de capital no local são bastante reduzidos e substituídos por um modelo de computação utilitária que é escalado com base na demanda de carga de trabalho.
* Cumpra consistentemente a autenticação acionada por política para seus serviços e APIs com uma anotação simples de Ingress. Com a segurança declarativa, é possível assegurar a autenticação do usuário e a validação do token usando o {{site.data.keyword.appid_short_notm}}.

**Etapa 2: operações e conexões para os sistemas de pagamento existentes de backend**
* Use o {{site.data.keyword.SecureGateway}} da IBM para manter conexões seguras com os sistemas de ferramentas locais restantes.
* Forneça painéis e práticas padronizados do DevOps por meio do Kubernetes.
* Depois que os desenvolvedores constroem e testam os apps nos clusters de Desenvolvimento e Teste, eles usam as cadeias de ferramentas do {{site.data.keyword.contdelivery_full}} para implementar apps nos clusters do Red Hat OpenShift on IBM Cloud em todo o mundo.
* As ferramentas de HA integradas no Red Hat OpenShift on IBM Cloud equilibram a carga de trabalho dentro de cada região geográfica, incluindo a capacidade de recuperação automática e o balanceamento de carga.

** Etapa 3: Analisar e evitar fraude **
* Implemente o IBM {{site.data.keyword.watson}} for Financial Services para evitar e detectar fraude.
* Usando as cadeias de ferramentas e as ferramentas de implementação do Helm, os apps também são implementados nos clusters do Red Hat OpenShift on IBM Cloud em todo o mundo. As cargas de trabalho e os dados atendem, então, às regulamentações regionais.

** Resultados **
* Levantar as VMs monolíticas existentes em contêineres hospedados em nuvem foi uma primeira etapa que permitiu ao Exec de Desenvolvimento economizar em custos de capital e de operações.
* Com o gerenciamento de infraestrutura resolvido pela IBM, a equipe de Desenvolvimento foi liberada para entregar atualizações 10 vezes diariamente.
* Em paralelo, o provedor implementou iterações de prazo fechado simples para obter um identificador na dívida técnica existente.
* Com o número de transações processadas, eles podem escalar suas operações exponencialmente.
* Ao mesmo tempo, uma nova análise de fraude com o {{site.data.keyword.watson}} aumentou a velocidade de detecção e prevenção, reduzindo a fraude 4 vezes mais do que a média da região.


