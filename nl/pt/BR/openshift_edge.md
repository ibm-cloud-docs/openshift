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

# Restringindo o tráfego de rede para os nós do trabalhador de borda
{: #edge}

Os nós do trabalhador de borda podem melhorar a segurança de seu cluster do {{site.data.keyword.openshiftlong}}, permitindo que menos nós do trabalhador sejam acessados externamente e isolando a carga de trabalho de rede.
{:shortdesc}

Quando esses nós do trabalhador são marcados somente para rede, outras cargas de trabalho não podem consumir a CPU ou memória do nó do trabalhador e interferir na rede.

Se você tiver um cluster de multizona e desejar restringir o tráfego de rede para nós do trabalhador de borda, pelo menos dois nós do trabalhador de borda deverão ser ativados em cada zona para alta disponibilidade de pods do balanceador de carga ou do Ingress. Crie um conjunto de trabalhadores do nó de borda que abranja todas as zonas em seu cluster, com pelo menos dois nós do trabalhador por zona.
{: tip}

## Identificação de nós do trabalhador como nós de borda
{: #edge_nodes}

Inclua o rótulo `dedicated=edge` em dois ou mais nós do trabalhador em cada VLAN pública ou privada em seu cluster para assegurar que os balanceadores de carga de rede (NLBs) e os balanceadores de carga do aplicativo (ALBs) do Ingress sejam implementados somente nesses nós do trabalhador.
{:shortdesc}

**Clusters Kubernetes da comunidade**: no Kubernetes 1.14 e mais recente, os NLBs e os ALBs privados e privados podem ser implementados nos nós do trabalhador de borda. No Kubernetes 1.13 e anteriores, os ALBs públicos e privados e os NLBs públicos podem ser implementados em nós de borda, mas os NLBs privados devem ser implementados em nós do trabalhador que não são de borda somente em seu cluster.
{: note}

Antes de iniciar:

* Assegure-se de que você tenha as seguintes [funções do {{site.data.keyword.cloud_notm}} IAM](/docs/containers?topic=containers-users#platform):
  * Qualquer função da plataforma para o cluster
  * Função de serviço **Gravador** ou **Gerenciador** para todos os namespaces
* [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

</br>Para rotular nós do trabalhador como nós de borda:

1. [Crie um novo conjunto de trabalhadores](/docs/containers?topic=containers-add_workers#add_pool) que abranja todas as zonas em seu cluster e tenha pelo menos dois trabalhadores por zona. No comando `ibmcloud oc worker-pool-create`, inclua a sinalização `--labels dedicated=edge` para rotular todos os nós do trabalhador no conjunto. Todos os nós do trabalhador nesse conjunto, incluindo quaisquer nós do trabalhador que forem incluídos posteriormente, serão rotulados como nós de borda. Após o conjunto de trabalhadores ser marcado com `dedicated=edge`, todos os nós do trabalhador existentes e subsequentes obterão esse rótulo e o Ingress e os balanceadores de carga serão implementados em um nó do trabalhador de borda.
  <p class="tip">Se você desejar usar um conjunto de trabalhadores existente, o conjunto deverá abranger todas as zonas em seu cluster e ter pelo menos dois trabalhadores por zona. É possível rotular o conjunto de trabalhadores com `dedicated=edge` usando a [API do conjunto de trabalhadores PATCH](https://containers.cloud.ibm.com/global/swagger-global-api/#/clusters/PatchWorkerPool). No corpo da solicitação, passe o JSON a seguir.
      <pre class="screen">
      {
        "labels": {"dedicated":"edge"},
        "state": "labels"
      }</pre></p>

2. Verifique se o conjunto de trabalhadores e os nós do trabalhador têm o rótulo `dedicated=edge`.
  * Para verificar o conjunto de trabalhadores:
    ```
    ibmcloud oc worker-pool-get --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
    ```
    {: pre}

  * Para verificar os nós do trabalhador individuais, revise o campo **Rótulos** da saída do comando a seguir.
    ```
    oc describe node <worker_node_private_IP>
    ```
    {: pre}

3. Recupere todos os NLBs e ALBs existentes no cluster.
  ```
  oc get services --all-namespaces | grep LoadBalancer
  ```
  {: pre}

  Na saída, anote o **Namespace** e o **Nome** de cada serviço de balanceador de carga. Por exemplo, na saída a seguir, há quatro serviços de balanceador de carga: um NLB público no namespace `default` e um privado e dois ALBs públicos no namespace `kube-system`.
  ```
  NAMESPACE     NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
  default       webserver-lb                                     LoadBalancer   172.21.190.18    169.46.17.2     80:30597/TCP                                10m
  kube-system   private-crdf253b6025d64944ab99ed63bb4567b6-alb1  LoadBalancer   172.21.158.78    10.185.94.150   80:31015/TCP,443:31401/TCP,9443:32352/TCP   25d
  kube-system   public-crdf253b6025d64944ab99ed63bb4567b6-alb1   LoadBalancer   172.21.84.248    169.48.228.78   80:30286/TCP,443:31363/TCP                  25d
  kube-system   public-crdf253b6025d64944ab99ed63bb4567b6-alb2   LoadBalancer   172.21.229.73    169.46.17.6     80:31104/TCP,443:31138/TCP                  25d
  ```
  {: screen}

4. Usando a saída da etapa anterior, execute o comando a seguir para cada NLB e ALB. Esse comando reimplementa o NLB ou ALB em um nó do trabalhador de borda.

  **Clusters Kubernetes da comunidade**: se o seu cluster executar o Kubernetes 1.14 ou mais recente, será possível implementar NLBs e ALBs públicos e privados para os nós do trabalhador de borda. No Kubernetes 1.13 e anterior, somente os ALBs públicos e privados e os NLBs públicos podem ser implementados em nós de borda, portanto, não reimplemente os serviços NLB privados.
  {: note}

  ```
  oc get service -n <namespace> <service_name> -o yaml | oc apply -f -
  ```
  {: pre}

  Saída de exemplo:
  ```
  service "webserver-lb" configured
  ```
  {: screen}

5. Para verificar se as cargas de trabalho de rede estão restritas aos nós de borda, confirme se os pods do NLB e ALB estão planejados para os nós de borda e não estão planejados para os nós que não são de borda.

  * Pods do NLB:
    1. Confirme se os pods do NLB são implementados em nós de borda. Procure o endereço IP externo do serviço de balanceador de carga que está listado na saída da etapa 3. Substitua os pontos (`.`) por hifens (`-`). Exemplo para o NLB `webserver-lb` que tem um endereço IP externo de `169.46.17.2`:
      ```
      oc describe nodes -l dedicated=edge | grep "169-46-17-2"
      ```
      {: pre}

      Saída de exemplo:
      ```
      ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
      ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
      ```
      {: screen}
    2. Confirme se nenhum pod do NLB é implementado em nós que não são de borda. Exemplo para o NLB `webserver-lb` que tem um endereço IP externo de `169.46.17.2`:
      ```
      oc describe nodes -l dedicated!=edge | grep "169-46-17-2"
      ```
      {: pre}
      * Se os pods do NLB forem implementados corretamente nos nós de borda, nenhum pod do NLB será retornado. Seus NLBs serão reagendados com êxito somente para os nós do trabalhador de borda.
      * Se os pods do NLB forem retornados, continue com a próxima etapa.

  * Pods do ALB:
    1. Confirme se todos os pods do ALB são implementados em nós de borda. Procure a palavra-chave `alb`. Cada ALB público e privado tem dois pods. Exemplo:
      ```
      oc describe nodes -l dedicated=edge | grep alb
      ```
      {: pre}

      Saída de exemplo para um cluster com duas zonas nas quais um ALB privado padrão e dois ALBs públicos padrão estão ativados:
      ```
      kube-system                private-crdf253b6025d64944ab99ed63bb4567b6-alb1-d5dd478db-27pv4    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                private-crdf253b6025d64944ab99ed63bb4567b6-alb1-d5dd478db-7p9q6    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb1-5ff8cdff89-s77z6    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb1-5ff8cdff89-kvs9f    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb2-57df7c7b5b-tp6xw    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      kube-system                public-crdf253b6025d64944ab99ed63bb4567b6-alb2-57df7c7b5b-z5p2v    0 (0%)        0 (0%)      0 (0%)           0 (0%)
      ```
      {: screen}

    2. Confirme se nenhum pod do ALB é implementado em nós que não são de borda. Exemplo:
      ```
      oc describe nodes -l dedicated!=edge | grep alb
      ```
      {: pre}
      * Se os pods do ALB forem implementados corretamente em nós de borda, nenhum pod do ALB será retornado. Seus ALBs serão reagendados com êxito somente para os nós do trabalhador de borda.
      * Se os pods do ALB forem retornados, continue com a próxima etapa.

6. Se os pods do NLB ou do ALB ainda estiverem implementados em nós que não são de borda, será possível excluir os pods para que eles sejam reimplementados em nós de borda. **Importante**: exclua somente um pod por vez e verifique se o pod é reagendado em um nó de borda antes de excluir outros pods.
  1. Excluir um pod. Exemplo se um dos pods do NLB `webserver-lb` não planejou para um nó de borda:
    ```
    oc delete pod ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg
    ```
    {: pre}

  2. Verifique se o pod é reagendado para um nó do trabalhador de borda. O reagendamento é automático, mas pode levar alguns minutos. Exemplo para o NLB `webserver-lb` que tem um endereço IP externo de `169.46.17.2`:
    ```
    oc describe nodes -l dedicated=edge | grep "169-46-17-2"
    ```
    {: pre}

    Saída de exemplo:
    ```
    ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-wz6dg                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
    ibm-system                 ibm-cloud-provider-ip-169-46-17-2-76fcb4965d-2z64r                 5m (0%)       0 (0%)      10Mi (0%)        0 (0%)
    ```
    {: screen}

</br>Você rotulou nós do trabalhador em um conjunto de trabalhadores com `dedicated=edge` e reimplementou todos os ALBs e NLBs existentes nos nós de borda. Todos os ALBs e NLBs subsequentes que forem incluídos no cluster também serão implementados em um nó de borda em seu conjunto de trabalhadores de borda. Em seguida, evite que outras [cargas de trabalho sejam executadas em nós do trabalhador de borda](#edge_workloads) e [bloqueiem o tráfego de entrada para NodePorts em nós do trabalhador](/docs/containers?topic=containers-network_policies#block_ingress).

<br />


## Evitando que cargas de trabalho sejam executadas em nós do trabalhador de borda
{: #edge_workloads}

Um benefício de nós do trabalhador de borda é que eles podem ser especificados para executar somente serviços de rede.
{:shortdesc}

Usar a tolerância `dedicated=edge` significa que todos os serviços de balanceador de carga de rede (NLB) e balanceador de carga do aplicativo (ALB) do Ingress são implementados somente nos nós do trabalhador rotulados. No entanto, para evitar que outras cargas de trabalho sejam executadas em nós do trabalhador de borda e consumam recursos do nó do trabalhador, deve-se usar [contaminações do Kubernetes ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/).

Antes de iniciar:
- Assegure-se de que você tenha a [função de serviço **Gerenciador** do {{site.data.keyword.cloud_notm}} IAM para todos os namespaces](/docs/containers?topic=containers-users#platform).
- [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

</br>Para evitar que outras cargas de trabalho sejam executadas em nós do trabalhador de borda:

1. Aplique uma contaminação a todos os nós do trabalhador com o rótulo `dedicated=edge` que evita que os pods sejam executados no nó do trabalhador e que remove os pods que não têm o rótulo `dedicated=edge` do nó do trabalhador. Os pods removidos são reimplementados em outros nós do trabalhador com capacidade.
  ```
  oc taint node -l dedicated=edge dedicated=edge:NoSchedule dedicated=edge:NoExecute
  ```
  {: pre}
  Agora, somente pods com a tolerância `dedicated=edge` são implementados em nós do trabalhador de borda.

2. Verifique se os nós de borda estão contaminados.
  ```
  oc describe nodes -l dedicated=edge | grep "Taint|Hostname"
  ```
  {: pre}

  Saída de exemplo:
  ```
  Taints:             dedicated=edge:NoExecute
    Hostname:    10.176.48.83
  Taints:             dedicated=edge:NoExecute
    Hostname:    10.184.58.7
  ```
  {: screen}

3. Se você escolher [ativar a preservação do IP de origem para um serviço NLB 1.0](/docs/containers?topic=containers-loadbalancer#node_affinity_tolerations), assegure-se de que os pods de app sejam planejados para os nós do trabalhador de borda [incluindo a afinidade do nó de borda em pods de app](/docs/containers?topic=containers-loadbalancer#lb_edge_nodes). Os pods do app devem ser planejados nos nós de borda para obter solicitações recebidas.

4. Para remover uma contaminação, execute o comando a seguir.
    ```
    oc taint node <node_name> dedicated:NoSchedule- dedicated:NoExecute-
    ```
    {: pre}


