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

# Abrindo portas e endereços IP necessários em seu firewall
{: #firewall}

Revise essas situações nas quais você pode precisar abrir portas e endereços IP específicos em seus firewalls para seus clusters do {{site.data.keyword.openshiftlong}}.
{:shortdesc}

* [Para executar comandos `ibmcloud` e `ibmcloud oc`](#firewall_bx) por meio de seu sistema local quando as políticas de rede corporativa impedem o acesso a terminais de Internet pública via proxies ou firewalls.
* [Para executar comandos `oc`](#firewall_kubectl) por meio do seu sistema local quando políticas de rede corporativa impedem o acesso a terminais de Internet pública via proxies ou firewalls.
* [Para executar comandos `calicoctl` ](#firewall_calicoctl)de seu sistema local quando as políticas de rede corporativa impedem o acesso aos terminais de Internet pública por meio de proxies ou de firewalls.
* [Para permitir a comunicação entre o mestre e os nós do trabalhador](#firewall_outbound) quando um firewall é configurado para os nós do trabalhador ou as configurações de firewall são customizadas em sua conta de infraestrutura do IBM Cloud.
* [Para permitir que o cluster acesse recursos por meio de um firewall na rede privada](#firewall_private).
* [Para permitir que o cluster acesse recursos quando as políticas de rede do Calico bloqueiam a saída do nó do trabalhador público ou privado](#firewall_calico_egress).
* [Para acessar o serviço NodePort, o serviço de balanceador de carga ou o Ingress de fora do cluster](#firewall_inbound).
* [Para permitir que o cluster acesse serviços que são executados dentro ou fora do {{site.data.keyword.cloud_notm}} ou localmente e são protegidos por um firewall](#whitelist_workers).

<br />


## Executando comandos `ibmcloud` e `ibmcloud oc` por trás de um firewall
{: #firewall_bx}

Se as políticas de rede corporativa impedirem o acesso de seu sistema local a terminais públicos via proxies ou firewalls, para executar comandos `ibmcloud` e `ibmcloud oc`, você deverá permitir o acesso TCP para {{site.data.keyword.cloud_notm}} e Red Hat OpenShift on IBM Cloud.
{:shortdesc}

1. Permita acesso a `cloud.ibm.com` na porta 443 em seu firewall.
2. Verifique sua conexão efetuando login no {{site.data.keyword.cloud_notm}} por meio desse terminal de API.
  ```
  ibmcloud login -a https://cloud.ibm.com/
  ```
  {: pre}
3. Permita acesso a `containers.cloud.ibm.com` na porta 443 em seu firewall.
4. Verifique sua conexão. Se o acesso for configurado corretamente, navios serão exibidos na saída.
   ```
   curl https://containers.cloud.ibm.com/v1/
   ```
   {: pre}

   Saída de exemplo:
   ```
                                     )___(
                              _______/__/_
                     ___     /===========|   ___
    ____       __   [\\\]___/____________|__[///]   __
    \   \_____[\\]__/___________________________\__[//]___
     \                                                    |
      \                                                  /
   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

   ```
   {: screen}

<br />


## Executando comandos `oc` por trás de um firewall
{: #firewall_kubectl}

Se as políticas de rede corporativa impedirem o acesso de seu sistema local a terminais públicos via proxies ou firewalls, para executar comandos `oc`, você deverá permitir o acesso TCP para o cluster.
{:shortdesc}

Quando um cluster é criado, a porta nas URLs do terminal em serviço é designada aleatoriamente entre 20000 e 32767. É possível escolher abrir o intervalo de portas 20000 a 32767 para qualquer cluster que pode ser criado ou é possível escolher permitir o acesso a um cluster existente específico.

Antes de iniciar, permita acesso para [executar comandos `ibmcloud oc`](#firewall_bx).

Para permitir acesso para um cluster específico:

1. Efetue login na CLI do {{site.data.keyword.cloud_notm}}. Insira suas credenciais do {{site.data.keyword.cloud_notm}} quando solicitadas. Se você tiver uma conta federada, inclua a opção `--sso`.

   ```
   ibmcloud login [ -- sso ]
   ```
   {: pre}

2. Se o cluster estiver em um grupo de recursos diferente de `default`, destine esse grupo de recursos. Para ver o grupo de recursos ao qual cada cluster pertence, execute `ibmcloud oc clusters`. **Nota**: deve-se ter pelo menos a função [**Visualizador**](/docs/containers?topic=containers-users#platform) para o grupo de recursos.
   ```
   ibmcloud target -g <resource_group_name>
   ```
   {: pre}

4. Obtenha o nome do cluster.

   ```
   ibmcloud oc clusters
   ```
   {: pre}

5. Recupere as URLs do terminal em serviço para seu cluster.
 * Se apenas a **URL do terminal em serviço público** estiver preenchida, obtenha essa URL. Seus usuários de cluster autorizados podem acessar o mestre por meio desse terminal na rede pública.
 * Se apenas a **URL do terminal em serviço privado** estiver preenchida, obtenha essa URL. Seus usuários de cluster autorizados podem acessar o mestre por meio desse terminal na rede privada.
 * Se a **URL do terminal em serviço público** e a **URL do terminal em serviço privado** estiverem preenchidas, obtenha as duas URLs. Os usuários de cluster autorizados podem acessar o mestre por meio do terminal público na rede pública ou no terminal privado na rede privada.

  ```
  ibmcloud oc cluster-get --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Saída de exemplo:
  ```
  ...
  Public Service Endpoint URL:    https://c3.<region>.containers.cloud.ibm.com:30426
  Private Service Endpoint URL:   https://c3-private.<region>.containers.cloud.ibm.com:31140
  ...
  ```
  {: screen}

6. Permita acesso às URLs e portas de terminal em serviço que você recebeu na etapa anterior. Se seu firewall for baseado em IP, será possível ver quais endereços IP são abertos quando você permite o acesso às URLs de terminal em serviço, revisando [esta tabela](#master_ips).

7. Verifique sua conexão.
  * Se o terminal em serviço público estiver ativado:
    ```
    curl -- insecure < public_service_endpoint_URL> /version
    ```
    {: pre}

    Exemplo de comando:
    ```
    curl --insecure https://c3.<region>.containers.cloud.ibm.com:31142/version
    ```
    {: pre}

    Saída de exemplo:
    ```
    {
     "major": "1",
     "minor": "7+",
     "gitVersion": "v1.7.4-2+eb9172c211dc41",
     "gitCommit": "eb9172c211dc4108341c0fd5340ee5200f0ec534",
     "gitTreeState": "clean",
     "buildDate": "2017-11-16T08:13:08Z",
     "goVersion": "go1.8.3",
     "compiler": "gc",
     "platform": "linux/amd64"
   }
    ```
    {: screen}
  * Se o terminal em serviço privado está ativado, deve-se estar em sua rede privada do {{site.data.keyword.cloud_notm}} ou conectar-se à rede privada por meio de uma conexão VPN para verificar sua conexão com o principal. **Nota**: deve-se [expor o terminal do mestre por meio de um balanceador de carga privado](/docs/containers?topic=containers-clusters#access_on_prem) para que os usuários possam acessar o mestre por meio de uma VPN ou uma conexão {{site.data.keyword.BluDirectLink}}.
    ```
    curl -- insecure < private_service_endpoint_URL> /version
    ```
    {: pre}

    Exemplo de comando:
    ```
    curl -- insecure https://c3-private. < region> .containers.cloud.ibm.com: 31142/version
    ```
    {: pre}

    Saída de exemplo:
    ```
    {
     "major": "1",
     "minor": "7+",
     "gitVersion": "v1.7.4-2+eb9172c211dc41",
     "gitCommit": "eb9172c211dc4108341c0fd5340ee5200f0ec534",
     "gitTreeState": "clean",
     "buildDate": "2017-11-16T08:13:08Z",
     "goVersion": "go1.8.3",
     "compiler": "gc",
     "platform": "linux/amd64"
   }
    ```
    {: screen}

8. Opcional: repita essas etapas para cada cluster que você precisa expor.

<br />


## Executando comandos `calicoctl` por trás de um firewall
{: #firewall_calicoctl}

Se as políticas de rede corporativa impedem o acesso de seu sistema local a terminais públicos por proxies ou firewalls, para executar comandos `calicoctl`, deve-se permitir acesso TCP aos comandos do Calico.
{:shortdesc}

Antes de iniciar, permita acesso para executar [comandos `ibmcloud`](#firewall_bx) e [comandos `oc`](#firewall_kubectl).

1. Recupere o endereço IP da URL principal que você usou para permitir os [comandos `oc`](#firewall_kubectl).

2. Obtenha a porta para etcd.

  ```
  oc get cm -n kube-system cluster-info -o yaml | grep etcd_host
  ```
  {: pre}

3. Permita acesso para as políticas do Calico por meio do endereço IP da URL do mestre e da porta etcd.

<br />


## Permitindo que o cluster acesse recursos de infraestrutura e outros serviços por um firewall público
{: #firewall_outbound}

Permita que seu cluster acesse recursos e serviços de infraestrutura por detrás de um firewall público, como para regiões do Red Hat OpenShift on IBM Cloud, o {{site.data.keyword.registrylong_notm}}, o {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM), o {{site.data.keyword.monitoringlong_notm}}, o {{site.data.keyword.loganalysislong_notm}}, os IPs privados de infraestrutura do IBM Cloud e a saída para solicitações de volume persistente.
{:shortdesc}

Deseja usar as políticas do Calico para agir como um firewall de cluster em vez de um firewall de dispositivo de gateway? Consulte [Isolando clusters na rede pública](/docs/containers?topic=containers-network_policies#isolate_workers_public).
{: tip}

Dependendo da configuração do cluster, você acessa os serviços usando os endereços IP público, privado ou ambos. Se você tiver um cluster com nós do trabalhador em VLANs públicas e privadas atrás de um firewall para as redes públicas e privadas, deverá abrir a conexão para endereços IP públicos e privados. Se o seu cluster tiver nós do trabalhador apenas na VLAN privada atrás de um firewall, será possível abrir a conexão apenas com os endereços IP privados.
{: note}

1.  Anote o endereço IP público para todos os nós do trabalhador no cluster.

    ```
    ibmcloud oc workers --cluster <cluster_name_or_ID>
    ```
    {: pre}

2.  Permita tráfego de rede de saída da origem <em>&lt;each_worker_node_publicIP&gt;</em> para o intervalo de portas TCP/UDP de destino 20000 a 32767 e a porta 443 e os seguintes endereços IP e grupos de rede. Esses endereços IP permitem que os nós do trabalhador se comuniquem com o cluster principal. Se você tiver um firewall corporativo que evita que sua máquina local acesse terminais de Internet pública, execute essa etapa também para sua máquina local, para que seja possível acessar o cluster principal.

    Deve-se permitir o tráfego de saída para a porta 443 para todas as zonas dentro da região para balancear a carga durante o processo de autoinicialização. Por exemplo, se seu cluster estiver no Sul dos EUA, o tráfego dos IPs públicos de cada um dos nós do trabalhador deverá ser permitido para a porta 443 do endereço IP para todas as zonas.
    {: important}

    {: #master_ips}
    <table summary="A primeira linha na tabela abrange ambas as colunas. O restante das linhas deve ser lido da esquerda para a direita, com a zona do servidor na coluna um e os endereços IP para corresponder na coluna dois.">
    <caption>Endereços IP a serem abertos para o tráfego de saída</caption>
          <thead>
          <th>Região</th>
          <th>Zona</th>
          <th>Endereço IP público</th>
          <th>Endereço IP Privado</th>
          </thead>
        <tbody>
          <tr>
            <td>AP Norte</td>
            <td>che01<br>hkg02<br>seo01<br>sng01<br><br>tok02, tok04, tok05</td>
            <td><code>169.38.70.10</code><br><code>169.56.132.234</code><br><code>169.56.69.242</code><br><code>161.202.186.226</code><br><br><code>161.202.126.210, 128.168.71.117, 165.192.69.69</code></td>
            <td><code>166.9.40.7</code><br><code> 166.9.42.7 </code><br><code> 166.9.44.5 </code><br><code> 166.9.40.8 </code><br><br><code> 166.9.40.6, 166.9.42.6, 166.9.44.4 </code></td>
           </tr>
          <tr>
             <td>AP Sul</td>
             <td>mel01<br><br>syd01, syd04, syd05</td>
             <td><code>168.1.97.67</code><br><br><code>168.1.8.195, 130.198.66.26, 168.1.12.98, 130.198.64.19</code></td>
             <td><code> 166.9.54.10 </code><br><br><code> 166.9.52.14, 166.9.52.15, 166.9.54.11, 166.9.54.13, 166.9.54.12 </code></td>
          </tr>
          <tr>
             <td>União Europeia Central</td>
             <td>ams03<br>mil01<br>osl01<br>par01<br><br>fra02, fra04, fra05</td>
             <td><code>169.50.169.110, 169.50.154.194</code><br><code> 159.122.190.98, 159.122.141.69 </code><br><code> 169.51.73.50 </code><br><code>159.8.86.149, 159.8.98.170</code><br><br><code>169.50.56.174, 161.156.65.42, 149.81.78.114</code></td>
             <td><code> 166.9.28.17, 166.9.30.11 </code><br><code> 166.9.28.20, 166.9.30.12 </code><br><code> 166.9.32.8 </code><br><code>166.9.28.19, 166.9.28.22</code><br><br><code>	166.9.28.23, 166.9.30.13, 166.9.32.9 </code></td>
            </tr>
          <tr>
            <td>Sul do Reino Unido</td>
            <td>lon02, lon04, lon05, lon06</td>
            <td><code>159.122.242.78, 158.175.111.42, 158.176.94.26, 159.122.224.242, 158.175.65.170, 158.176.95.146</code></td>
            <td><code>166.9.34.5, 166.9.34.6, 166.9.36.10, 166.9.36.11, 166.9.36.12, 166.9.36.13, 166.9.38.6, 166.9.38.7</code></td>
          </tr>
          <tr>
            <td>Leste dos EUA</td>
             <td>mon01<br>tor01<br><br>wdc04, wdc06, wdc07</td>
             <td><code>169.54.126.219</code><br><code>169.53.167.50</code><br><br><code>169.63.88.186, 169.60.73.142, 169.61.109.34, 169.63.88.178, 169.60.101.42, 169.61.83.62</code></td>
             <td><code> 166.9.20.11 </code><br><code> 166.9.22.8 </code><br><br><code> 166.9.20.12, 166.9.20.13, 166.9.22.9, 166.9.22.10, 166.9.24.4, 166.9.24.5 </code></td>
          </tr>
          <tr>
            <td>SUL dos EUA</td>
            <td>hou02<br>mex01<br>sao01<br>sjc03<br>sjc04<br><br>dal10,dal12,dal13</td>
            <td><code>184.173.44.62</code><br><code> 169.57.100.18 </code><br><code>169.57.151.10</code><br><code> 169.45.67.210 </code><br><code> 169.62.82.197 </code><br><br><code>169.46.7.238, 169.48.230.146, 169.61.29.194, 169.46.110.218, 169.47.70.10, 169.62.166.98, 169.48.143.218, 169.61.177.2, 169.60.128.2</code></td>
            <td><code> 166.9.15.74 </code><br><code> 166.9.15.76 </code><br><code> 166.9.12.143 </code><br><code> 166.9.12.144 </code><br><code>166.9.15.75</code><br><br><code>166.9.12.140, 166.9.12.141, 166.9.12.142, 166.9.15.69, 166.9.15.70, 166.9.15.72, 166.9.15.71, 166.9.15.73, 166.9.16.183, 166.9.16.184, 166.9.16.185</code></td>
          </tr>
          </tbody>
        </table>

3.  {: #firewall_registry}Para permitir que os nós do trabalhador se comuniquem com o {{site.data.keyword.registrylong_notm}}, permita o tráfego de rede de saída dos nós do trabalhador para [regiões do {{site.data.keyword.registrylong_notm}}](/docs/services/Registry?topic=registry-registry_overview#registry_regions):
  - `TCP port 443, port 4443 FROM <each_worker_node_publicIP> TO <registry_subnet>`
  -  Substitua <em>&lt;registry_subnet&gt;</em> pela sub-rede de registro para a qual você deseja permitir o tráfego. O registro global armazena imagens públicas fornecidas pela IBM e os registros regionais armazenam suas próprias imagens privadas ou públicas. A porta 4443 é necessária para funções de tabelião público, como [Verificando assinaturas de imagem](/docs/services/Registry?topic=registry-registry_trustedcontent#registry_trustedcontent). <table summary="A primeira linha na tabela abrange ambas as colunas. O restante das linhas deve ser lido da esquerda para a direita, com a zona do servidor na coluna um e os endereços IP para corresponder na coluna dois.">
  <caption>Endereços IP a serem abertos para o tráfego de Registro</caption>
    <thead>
      <th>Região do Red Hat OpenShift on IBM Cloud</th>
      <th>Endereço de registro</th>
      <th>Sub-redes públicas de registro</th>
      <th>Endereços IP privados de registro</th>
    </thead>
    <tbody>
      <tr>
        <td>Registro global em <br>Regiões do Red Hat OpenShift on IBM Cloud</td>
        <td><code>icr.io</code><br><br>
        Descontinuado:  <code> registry.bluemix.net </code></td>
        <td><code>169.60.72.144/28</code></br><code>169.61.76.176/28</code></br><code>169.62.37.240/29</code></br><code>169.60.98.80/29</code></br><code>169.63.104.232/29</code></td>
        <td><code>166.9.20.4</code></br><code>166.9.22.3</code></br><code>166.9.24.2</code></td>
      </tr>
      <tr>
        <td>AP Norte</td>
        <td><code>jp.icr.io</code><br><br>
        Descontinuado:  <code> registry.au-syd.bluemix.net </code></td>
        <td><code>161.202.146.86/29</code></br><code>128.168.71.70/29</code></br><code>165.192.71.222/29</code></td>
        <td><code>166.9.40.3</code></br><code>166.9.42.3</code></br><code>166.9.44.3</code></td>
      </tr>
      <tr>
        <td>AP Sul</td>
        <td><code>au.icr.io</code><br><br>
        Descontinuado:  <code> registry.au-syd.bluemix.net </code></td>
        <td><code>168.1.45.160/27</code></br><code>168.1.139.32/27</code></br><code>168.1.1.240/29</code></br><code>130.198.88.128/29</code></br><code>135.90.66.48/29</code></td>
        <td><code>166.9.52.2</code></br><code>166.9.54.2</code></br><code>166.9.56.3</code></td>
      </tr>
      <tr>
        <td>União Europeia Central</td>
        <td><code>de.icr.io</code><br><br>
        Descontinuado:  <code> registry.eu-de.bluemix.net </code></td>
        <td><code>169.50.56.144/28</code></br><code>159.8.73.80/28</code></br><code>169.50.58.104/29</code></br><code>161.156.93.16/29</code></br><code>149.81.79.152/29</code></td>
        <td><code>166.9.28.12</code></br><code>166.9.30.9</code></br><code>166.9.32.5</code></td>
       </tr>
       <tr>
        <td>Sul do Reino Unido</td>
        <td><code>uk.icr.io</code><br><br>
        Descontinuado:  <code> registry.eu-gb.bluemix.net </code></td>
        <td><code>159.8.188.160/27</code></br><code>169.50.153.64/27</code></br><code>158.175.97.184/29</code></br><code>158.176.105.64/29</code></br><code>141.125.71.136/29</code></td>
        <td><code>166.9.36.9</code></br><code>166.9.38.5</code></br><code>166.9.34.4</code></td>
       </tr>
       <tr>
        <td>Leste dos EUA, Sul dos EUA</td>
        <td><code>us.icr.io</code><br><br>
        Descontinuado:  <code> registry.ng.bluemix.net </code></td>
        <td><code>169.55.39.112/28</code></br><code>169.46.9.0/27</code></br><code>169.55.211.0/27</code></br><code>169.61.234.224/29</code></br><code>169.61.135.160/29</code></br><code>169.61.46.80/29</code></td>
        <td><code>166.9.12.114</code></br><code>166.9.15.50</code></br><code>166.9.16.173</code></td>
       </tr>
      </tbody>
    </table>

4. Permita o tráfego de rede de saída de seu nó do trabalhador para {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Seu firewall deve ser de Camada 7 para inserir o nome de domínio do IAM na lista de desbloqueio. O IAM não tem endereços IP específicos que você pode inserir na lista de desbloqueio. Se o firewall não suportar a Camada 7, será possível permitir todo o tráfego de rede HTTPS na porta 443.
    - `TCP port 443 FROM <each_worker_node_publicIP> TO https://iam.bluemix.net`
    - `TCP port 443 FROM <each_worker_node_publicIP> TO https://iam.cloud.ibm.com`

5. Opcional: permita o tráfego de rede de saída dos nós do trabalhador para os serviços {{site.data.keyword.monitoringlong_notm}}, {{site.data.keyword.loganalysislong_notm}}, Sysdig e LogDNA:
    *   **{{site.data.keyword.monitoringlong_notm}}**:
        <pre class="screen">TCP port 443, port 9095 FROM &lt;each_worker_node_public_IP&gt; TO &lt;monitoring_subnet&gt;</pre>
        Substitua <em>&lt;monitoring_subnet&gt;</em> pelas sub-redes para as regiões de monitoramento para as quais você deseja permitir o tráfego:
        <p><table summary="A primeira linha na tabela abrange ambas as colunas. O restante das linhas deve ser lido da esquerda para a direita, com a zona do servidor na coluna um e os endereços IP para corresponder na coluna dois.">
    <caption>Endereços IP a serem abertos para o tráfego de monitoramento</caption>
                <thead>
                <th>Região do {{site.data.keyword.containerlong_notm}}</th>
                <th>Endereço de monitoramento</th>
                <th>Monitorando sub-redes</th>
                </thead>
              <tbody>
                <tr>
                 <td>União Europeia Central</td>
                 <td><code>Metrics.eu-de.bluemix.net</code></td>
                 <td><code>158.177.65.80/30</code></td>
                </tr>
                <tr>
                 <td>Sul do Reino Unido</td>
                 <td><code>Metrics.eu-gb.bluemix.net</code></td>
                 <td><code>169.50.196.136/29</code></td>
                </tr>
                <tr>
                  <td>Leste dos EUA, Sul dos EUA, AP Norte, AP Sul</td>
                  <td><code>Metrics.ng.bluemix.net</code></td>
                  <td><code>169.47.204.128/29</code></td>
                 </tr>
                </tbody>
              </table></p>
    *   **{{site.data.keyword.mon_full_notm}}**:
        <pre class="screen">TCP port 443, port 6443 FROM &lt;each_worker_node_public_IP&gt; TO &lt;sysdig_public_IP&gt;</pre>
        Substitua `<sysdig_public_IP>` pelos [Endereços IP do Sysdig](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-network#network).
    *   **{{site.data.keyword.loganalysislong_notm}}**:
        <pre class="screen">TCP port 443, port 9091 FROM &lt;each_worker_node_public_IP&gt; TO &lt;logging_public_IP&gt;</pre>
        Substitua <em>&lt;logging_public_IP&gt;</em> por todos os endereços das regiões de criação de log para as quais você deseja permitir o tráfego:
        <p><table summary="A primeira linha na tabela abrange ambas as colunas. O restante das linhas deve ser lido da esquerda para a direita, com a zona do servidor na coluna um e os endereços IP para corresponder na coluna dois.">
    <caption>Endereços IP a serem abertos para o tráfego de criação de log</caption>
                <thead>
                <th>Região do {{site.data.keyword.containerlong_notm}}</th>
                <th>Endereço de criação de log</th>
                <th>Endereços IP de log</th>
                </thead>
                <tbody>
                  <tr>
                    <td>Leste dos EUA, Sul dos EUA</td>
                    <td><code>ingest.logging.ng.bluemix.net</code></td>
                    <td><code>169.48.79.236</code><br><code>169.46.186.113</code></td>
                  </tr>
                  <tr>
                   <td>Sul do Reino Unido</td>
                   <td><code>ingest.logging.eu-gb.bluemix.net</code></td>
                   <td><code>169.50.115.113</code></td>
                  </tr>
                  <tr>
                   <td>União Europeia Central</td>
                   <td><code>ingest-eu-fra.logging.bluemix.net</code></td>
                   <td><code>158.177.88.43</code><br><code>159.122.87.107</code></td>
                  </tr>
                  <tr>
                   <td>AP Sul, AP Norte</td>
                   <td><code>ingest-au-syd.logging.bluemix.net</code></td>
                   <td><code>130.198.76.125</code><br><code>168.1.209.20</code></td>
                  </tr>
                 </tbody>
               </table></p>
    *   **{{site.data.keyword.la_full_notm}}**:
        <pre class="screen">TCP port 443, port 80 FROM &lt;each_worker_node_public_IP&gt; TO &lt;logDNA_public_IP&gt;</pre>
        Substitua `<logDNA_public_IP>` pelos [endereços IP do LogDNA](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-network#network).

6. Se você usar os serviços do balanceador de carga, assegure-se de que todo o tráfego que usa o protocolo VRRP seja permitido entre os nós do trabalhador nas interfaces pública e privada. O Red Hat OpenShift on IBM Cloud usa o protocolo VRRP para gerenciar endereços IP para balanceadores de carga públicos e privados.

7. {: #pvc}Para criar solicitações de volume persistente em um cluster privado, certifique-se de que seu cluster esteja configurado com a versão do Kubernetes a seguir ou as versões de plug-in de armazenamento do {{site.data.keyword.cloud_notm}}. Essas versões ativam a comunicação de rede privada de seu cluster para suas instâncias de armazenamento persistente.
    <table>
    <caption>Visão geral das versões de plug-in de armazenamento do Kubernetes ou do {{site.data.keyword.cloud_notm}} necessárias para clusters privados</caption>
    <thead>
      <th>Tipo de armazenamento</th>
      <th>Versão necessária</th>
   </thead>
   <tbody>
     <tr>
       <td>Armazenamento de arquivo</td>
       <td>Kubernetes versão <code>1.13.4_1512</code>, <code>1.12.6_1544</code>, <code>1.11.8_1550</code>, <code>1.10.13_1551</code> ou mais recente</td>
     </tr>
     <tr>
       <td>Armazenamento de bloco</td>
       <td>Plug-in do {{site.data.keyword.cloud_notm}} Block Storage versão 1.3.0 ou mais recente</td>
     </tr>
     <tr>
       <td>Armazenamento de objetos</td>
       <td><ul><li>{{site.data.keyword.cos_full_notm}}  plug-in versão 1.0.3 ou mais recente</li><li>{{site.data.keyword.cos_full_notm}}  serviço configurado com autenticação HMAC</li></ul></td>
     </tr>
   </tbody>
   </table>

   Se precisar usar uma versão do Kubernetes ou uma versão de plug-in de armazenamento do {{site.data.keyword.cloud_notm}} que não suporta comunicação de rede por meio de uma rede privada ou se você desejar usar o {{site.data.keyword.cos_full_notm}} sem autenticação HMAC, permita o acesso de saída por meio de seu firewall para a infraestrutura do IBM Cloud e do {{site.data.keyword.cloud_notm}} Identity and Access Management:
   - Permitir todo o tráfego de rede de saída na porta TCP 443.
   - Permitir acesso ao intervalo de IP da infraestrutura do IBM Cloud para a zona em que seu cluster está na [**rede front-end (pública)**](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#frontend-public-network) e na [**rede back-end (privada)**](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#backend-private-network). Para localizar a zona do seu cluster, execute `ibmcloud oc clusters`.


<br />


## Permitindo que o cluster acesse recursos por meio de um firewall privado
{: #firewall_private}

Se você tiver um firewall na rede privada, permita a comunicação entre os nós do trabalhador e permita que seu cluster acesse recursos de infraestrutura por meio da rede privada.
{:shortdesc}

Deseja usar as políticas do Calico para agir como um firewall de cluster em vez de um firewall de dispositivo de gateway? Consulte [Isolando clusters na rede privada](/docs/containers?topic=containers-network_policies#isolate_workers).
{: tip}

1. Permitir todo o tráfego entre os nós do trabalhador.
    1. Permitir todo o tráfego TCP, UDP, VRRP e IPEncap entre os nós do trabalhador nas interfaces pública e privada. O Red Hat OpenShift on IBM Cloud usa o protocolo VRRP para gerenciar endereços IP para balanceadores de carga privados e o protocolo IPEncap para permitir o tráfego de pod para pod entre sub-redes.
    2. Se você usar políticas do Calico ou se tiver firewalls em cada zona de um cluster de múltiplas zonas, um firewall poderá bloquear a comunicação entre os nós do trabalhador. Deve-se abrir todos os nós do trabalhador no cluster entre si usando as portas dos trabalhadores, os endereços IP privados dos trabalhadores ou o rótulo do nó do trabalhador do Calico.

2. Permita os intervalos de IP privados da infraestrutura do IBM Cloud possam criar nós do trabalhador em seu cluster.
    1. Permita os intervalos IP privados de infraestrutura do IBM Cloud apropriados. Consulte  [ Rede de backend (privada) ](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#backend-private-network).
    2. Permita os intervalos de IP privado da infraestrutura do IBM Cloud para todas as [zonas](/docs/containers?topic=containers-regions-and-zones#zones) que você está usando. **Nota**: deve-se incluir IPs para as zonas `dal01`, `dal10`, `wdc04` e, se seu cluster está na geografia Europa, a zona `ams01`. Consulte  [ Rede de Serviço (na rede backend / privada) ](/docs/infrastructure/hardware-firewall-dedicated?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges#service-network-on-backend-private-network-).

3. Abra as portas a seguir:
    - Permita conexões TCP e UDP de saída dos trabalhadores para as portas 80 e 443 para permitir atualizações e recarregamentos do nó do trabalhador.
    - Permita TCP e UDP de saída para a porta 2049 para permitir o armazenamento de arquivo de montagem como volumes.
    - Permita TCP e UDP de saída para a porta 3260 para comunicação com o armazenamento de bloco.
    - Permita conexões TCP e UDP de entrada para a porta 10250 para o painel do OpenShift e comandos, como `oc logs` e `oc exec`.
    - Permita conexões de entrada e de saída para a porta TCP e UDP 53 para acesso de DNS.

4. Se você também tiver um firewall na rede pública ou se tiver um cluster de VLAN privado e estiver usando um dispositivo de gateway como um firewall, também deverá permitir os IPs e portas especificados em [Permitindo que o cluster acesse recursos de infraestrutura e outros serviços](#firewall_outbound).

<br />


## Permitindo que o cluster acesse recursos por meio de políticas de saída do Calico
{: #firewall_calico_egress}

Se você usar as [políticas de rede do Calico](/docs/containers?topic=containers-network_policies) para agir como um firewall para restringir todos os recursos do nó do trabalhador público, você deverá permitir que os nós do trabalhador acessem as sub-redes que são necessárias para que o cluster funcione.
{: shortdesc}

Para usar políticas do Calico para agir como seu firewall de cluster na rede pública, deve-se aplicar as políticas em [Isolando clusters na rede pública](/docs/containers?topic=containers-network_policies#isolate_workers_public).

Para usar políticas do Calico para agir como seu firewall de cluster na rede privada, deve-se aplicar as políticas em [Isolando clusters na rede privada](/docs/containers?topic=containers-network_policies#isolate_workers).

<br />


## Acessando o NodePort, o balanceador de carga e os serviços do Ingress de fora do cluster
{: #firewall_inbound}

É possível permitir acesso de entrada para o NodePort, o balanceador de carga e os serviços do Ingress.
{:shortdesc}

<dl>
  <dt>Serviço NodePort</dt>
  <dd>Abra a porta que você configurou quando implementou o serviço aos endereços IP públicos para todos os nós do trabalhador para permitir o tráfego. Para localizar a porta, execute `oc get svc`. A porta está no intervalo de 20000 a 32000.<dd>
  <dt>Serviço de balanceador de carga</dt>
  <dd>Abra a porta que você configurou quando implementou o serviço para o endereço IP público do serviço do balanceador de carga.</dd>
  <dt>Entrada</dt>
  <dd>Abra a porta 80 para HTTP ou a porta 443 para HTTPS para o endereço IP para o balanceador de carga do aplicativo Ingress.</dd>
</dl>

<br />


## Whitelisting seu cluster em firewalls de outros serviços ou em firewalls no local
{: #whitelist_workers}

Se você deseja acessar serviços que são executados dentro ou fora do {{site.data.keyword.cloud_notm}} ou no local e que são protegidos por um firewall, é possível incluir os endereços IP de seus nós do trabalhador nesse firewall para permitir o tráfego de rede de saída para seu cluster. Por exemplo, você pode desejar ler dados de um banco de dados do {{site.data.keyword.cloud_notm}} que é protegido por um firewall ou inserir suas sub-redes do nó do trabalhador na lista de desbloqueio em um firewall no local para permitir o tráfego de rede de seu cluster.
{:shortdesc}

1.  [Efetue login em sua conta. Se aplicável, direcione o grupo de recursos apropriado. Configure o contexto para o seu cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

2. Obtenha as sub-redes do nó do trabalhador ou os endereços IP do nó do trabalhador.
  * **Sub-redes do nó do trabalhador**: se você antecipar a mudança do número de nós do trabalhador em seu cluster frequentemente, como se você ativasse o [escalador automático de cluster](/docs/containers?topic=containers-ca#ca), talvez não desejará atualizar o firewall para cada novo nó do trabalhador. Em vez disso, é possível inserir na lista de desbloqueio as sub-redes VLAN que o cluster usa. Lembre-se que a sub-rede VLAN pode ser compartilhada pelos nós do trabalhador em outros clusters.
    <p class="note">As **sub-redes públicas primárias** que o Red Hat OpenShift on IBM Cloud provisiona para seu cluster são fornecidas com 14 endereços IP disponíveis e podem ser compartilhadas por outros clusters na mesma VLAN. Quando você tem mais de 14 nós do trabalhador, outra sub-rede é pedida, de modo que as sub-redes que você precisa inserir na lista de desbloqueio podem mudar. Para reduzir a frequência de mudança, crie conjuntos de trabalhadores com tipos de nó do trabalhador de recursos mais altos de CPU e memória para que você não precise incluir nós do trabalhador com frequência.</p>
    1. Liste os nós do trabalhador em seu cluster.
      ```
      ibmcloud oc workers --cluster <cluster_name_or_ID>
      ```
      {: pre}

    2. Na saída da etapa anterior, observe todos os IDs de rede exclusivos (primeiros três octetos) do **IP público** para os nós do trabalhador em seu cluster. Se você deseja incluir na lista de desbloqueio um cluster somente privado, anote o **IP privado** no lugar. Na saída a seguir, os IDs de rede exclusivos são `169.xx.178` e `169.xx.210`.
        ```
        ID                                                 Public IP        Private IP     Machine Type        State    Status   Zone    Version   
        kube-dal10-crb2f60e9735254ac8b20b9c1e38b649a5-w31   169.xx.178.101   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal10   1.13.8   
        kube-dal10-crb2f60e9735254ac8b20b9c1e38b649a5-w34   169.xx.178.102   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal10   1.13.8  
        kube-dal12-crb2f60e9735254ac8b20b9c1e38b649a5-w32   169.xx.210.101   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal12   1.13.8   
        kube-dal12-crb2f60e9735254ac8b20b9c1e38b649a5-w33   169.xx.210.102   10.xxx.xx.xxx   b3c.4x16.encrypted   normal   Ready    dal12   1.13.8  
        ```
        {: screen}
    3.  Liste as sub-redes VLAN para cada ID de rede exclusivo.
        ```
        ibmcloud sl subnet list | grep -e <networkID1> -e <networkID2>
        ```
        {: pre}

        Saída de exemplo:
        ```
        ID        identifier       type                 network_space   datacenter   vlan_id   IPs   hardware   virtual_servers
        1234567   169.xx.210.xxx   ADDITIONAL_PRIMARY   PUBLIC          dal12        1122334   16    0          5   
        7654321   169.xx.178.xxx   ADDITIONAL_PRIMARY   PUBLIC          dal10        4332211   16    0          6    
        ```
        {: screen}
    4.  Recupere o endereço da sub-rede. Na saída, localize o número de **IPs**. Em seguida, eleve `2` à potência de `n` igual ao número de IPs. Por exemplo, se o número de IPs for `16`, então `2` será elevado para a potência de `4` (`n`) para igual a `16`. Agora, obtenha o CIDR de sub-rede subtraindo o valor de `n` de `32` bits. Por exemplo, quando `n` é igual a `4`, então, o CIDR é `28` (da equação `32 - 4 = 28`). Combine a máscara **identificador** com o valor CIDR para obter o endereço completo da sub-rede. Na saída anterior, os endereços de sub-rede são:
        *   ` 169.xx.210.xxx/ 28 `
        *   ` 169.xx.178.xxx/ 28 `
  * **Endereços IP do nó do trabalhador individual**: se você tiver um pequeno número de nós do trabalhador que executam apenas um aplicativo e não precisar escalar ou se você desejar inserir na lista de desbloqueio apenas um nó do trabalhador, liste todos os nós do trabalhador em seu cluster e anote os endereços **IP públicos**. Se os nós do trabalhador estiverem conectados a uma rede privada apenas e você desejar se conectar a {{site.data.keyword.cloud_notm}} serviços usando o terminal em serviço privado, observe os endereços **IP Privado** em seu lugar. Apenas esses nós do trabalhador são incluídos na lista de desbloqueio. Se você excluir os nós do trabalhador ou incluir nós do trabalhador no cluster, deverá atualizar o firewall de acordo.
    ```
    ibmcloud oc workers --cluster <cluster_name_or_ID>
    ```
    {: pre}
4.  Inclua o CIDR da sub-rede ou os endereços IP no firewall de seu serviço para o tráfego de saída ou o firewall no local para o tráfego de entrada.
5.  Repita essas etapas para cada cluster que você deseja desistçar.


