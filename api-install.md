---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, roks, rhoks, rhos, api

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}



# Setting up the API
{: #cs_api_install}

{{site.data.keyword.openshiftlong}} shares the same application programming interface (API) as {{site.data.keyword.containerlong_notm}}, so that you can use the same methods to consistently create and manage your community Kubernetes or {{site.data.keyword.openshiftshort}} clusters. To use the CLI, see [Setting up the CLI](/docs/openshift?topic=openshift-openshift-cli).
{: shortdesc}

## About the API
{: #api_about}

The {{site.data.keyword.openshiftlong_notm}} API automates the provisioning and management of {{site.data.keyword.cloud_notm}} infrastructure resources for your clusters so that your apps have the compute, networking, and storage resources that they need to serve your users.
{: shortdesc}

The API is versioned to support the different infrastructure providers that are available for you to create clusters. For more information, see [Overview of Classic and VPC infrastructure providers](/docs/containers?topic=containers-infrastructure_providers).

You can use the version two (`v2`) API to manage both classic and VPC clusters. The `v2` API is designed to avoid breaking existing functionality when possible. However, make sure that you review the following differences between the `v1` and `v2` API.

<table summary="The rows are read from left to right, with the area of comparison in column one, version 1 API in column two, and version 2 API in column three.">
<caption>{{site.data.keyword.openshiftlong_notm}} API versions</caption>
<col width="20%">
<col width="40%">
<col width="40%">
    <thead>
    <th>Area</th>
    <th>v1 API</th>
    <th>v2 API</th>
    </thead>
    <tbody>
    <tr>
    <td>API endpoint prefix</td>
    <td><code>https://containers.cloud.ibm.com/global/v1</code></td>
    <td><code>https://containers.cloud.ibm.com/global/v2</code></td>
    </tr>
    <tr>
    <td>API reference docs</td>
    <td><a href="https://containers.cloud.ibm.com/global/swagger-global-api/#/"><code>https://containers.cloud.ibm.com/global/swagger-global-api/</code></a> <img src="../icons/launch-glyph.svg" alt="External link icon"></td>
    <td><a href="https://containers.cloud.ibm.com/global/swagger-global-api/#/"><code>https://containers.cloud.ibm.com/global/swagger-global-api/</code></a> <img src="../icons/launch-glyph.svg" alt="External link icon"></td>
    </tr>
    <tr>
    <td>API architectural style</td>
    <td>Representational state transfer (REST) that focuses on resources that you interact with through HTTP methods such as <code>GET</code>, <code>POST</code>, <code>PUT</code>, <code>PATCH</code>, and <code>DELETE</code>.</td>
    <td>Remote procedure calls (RPC) that focus on actions through only <code>GET</code> and <code>POST</code> HTTP methods.</td>
    </tr>
    <tr>
    <td>Supported container platforms</td>
    <td>Use the {{site.data.keyword.openshiftlong_notm}} API to manage your {{site.data.keyword.cloud_notm}} infrastructure resources, such as worker nodes, for <strong>both community Kubernetes and {{site.data.keyword.openshiftshort}} clusters</strong>.</td>
    <td>Use the {{site.data.keyword.openshiftlong_notm}} <code>v2</code> API to manage your {{site.data.keyword.cloud_notm}} infrastructure resources, such as worker nodes, for <strong>both community Kubernetes and {{site.data.keyword.openshiftshort}} VPC clusters</strong>.</td>
    </tr>
    <tr>
    <td>{{site.data.keyword.openshiftshort}} API</td>
    <td>To use the {{site.data.keyword.openshiftshort}} API to manage {{site.data.keyword.openshiftshort}} and Kubernetes resources within the cluster, such as pods or namespaces, you must log in by exchanging an {{site.data.keyword.cloud_notm}} API key for an {{site.data.keyword.openshiftshort}} access token. See <a href="/docs/openshift?topic=openshift-access_cluster#access_api_key">Using an API key to log in to clusters</a>.</td>
    <td>Same as <code>v1</code>; see <a href="/docs/openshift?topic=openshift-access_cluster#access_api_key">Using an API key to log in to clusters</a>.</td>
    </tr>
    <tr>
    <td>Supported infrastructure providers</td>
    <td><code>classic</code></td>
    <td><code>vpc</code> and <code>classic</code><ul>
    <li>The <code>vpc</code> provider is designed to support multiple VPC subproviders. The supported VPC subprovider is <code>vpc-gen2</code>, which corresponds to a VPC cluster for Generation 2 compute resources.</li>
    <li>Provider-specific requests have a path parameter in the URL, such as <code>v2/vpc/createCluster</code>. Some APIs are only available to a particular provider, such as <code>GET vlan</code> for classic or <code>GET vpcs</code> for VPC.</li>
    <li>Provider-neutral requests can include a provider-specific body parameter that you specify, usually in JSON, such as <code>{"provider": "vpc"}</code>, if you want to return responses for only the specified provider.</li></ul></td>
    </tr>
    <tr>
    <td><code>GET</code> responses</td>
    <td>The <code>GET</code> method for a collection of resources (such as <code>GET v1/clusters</code>) returns the same details for each resource in the list as a <code>GET</code> method for an individual resource (such as <code>GET v1/clusters/{idOrName}</code>).</td>
    <td>To return responses faster, the v2 <code>GET</code> method for a collection of resources (such as <code>GET v2/clusters</code>) returns only a subset of information that is detailed in a <code>GET</code> method for an individual resource (such as <code>GET v2/clusters/{idOrName}</code>).
    <br><br>Some list responses include a providers property to identify whether the returned item applies to classic or VPC infrastructure. For example, the <code>GET zones</code> list returns some results such as <code>mon01</code> that are available only in the classic infrastructure provider, while other results such as <code>us-south-01</code> are available only in the VPC infrastructure provider.</td>
    </tr>
    <tr>
    <td>Cluster, worker node, and worker-pool responses</td>
    <td>Responses include only information that is specific to the classic infrastructure provider, such as the VLANs in <code>GET</code> cluster and worker responses.</td>
    <td>The information that is returned varies depending on the infrastructure provider. For such provider-specific responses, you can specify the provider in your request. For example, VPC clusters do not return VLAN information since they do not have VLANs. Instead, they return subnet and CIDR network information.</td>
    </tr>
</tbody>
</table>




## Automating cluster deployments with the API
{: #cs_api}

You can use the {{site.data.keyword.openshiftlong_notm}} API to automate the creation, deployment, and management of your {{site.data.keyword.openshiftshort}} clusters.
{: shortdesc}


The {{site.data.keyword.openshiftlong_notm}} API requires header information that you must provide in your API request and that can vary depending on the API that you want to use. To determine what header information is needed for your API, see the [{{site.data.keyword.openshiftlong_notm}} API documentation](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external}.

To authenticate with {{site.data.keyword.openshiftlong_notm}}, you must provide an {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) token that is generated with your {{site.data.keyword.cloud_notm}} credentials and that includes the {{site.data.keyword.cloud_notm}} account ID where the cluster was created. Depending on the way you authenticate with {{site.data.keyword.cloud_notm}}, you can choose between the following options to automate the creation of your {{site.data.keyword.cloud_notm}} IAM token.

You can also use the [API swagger JSON file](https://containers.cloud.ibm.com/global/swagger-global-api/swagger.json){: external} to generate a client that can interact with the API as part of your automation work.
{: tip}

|{{site.data.keyword.cloud_notm}} ID|My options|
|-----------------------------------|----------|
|Unfederated ID|<ul><li><strong>Generate an {{site.data.keyword.cloud_notm}} API key:</strong> As an alternative to using the {{site.data.keyword.cloud_notm}} username and password, you can <a href="/docs/account?topic=account-userapikey#create_user_key">use {{site.data.keyword.cloud_notm}} API keys</a> <img src="../icons/launch-glyph.svg" alt="External link icon">. {{site.data.keyword.cloud_notm}} API keys are dependent on the {{site.data.keyword.cloud_notm}} account they are generated for. You cannot combine your {{site.data.keyword.cloud_notm}} API key with a different account ID in the same {{site.data.keyword.cloud_notm}} IAM token. To access clusters that were created with an account other than the one your {{site.data.keyword.cloud_notm}} API key is based on, you must log in to the account to generate a new API key.</li><li><strong>{{site.data.keyword.cloud_notm}} username and password:</strong> You can follow the steps in this topic to fully automate the creation of your {{site.data.keyword.cloud_notm}} IAM access token.</li></ul>|
|Federated ID|<ul><li><strong>Generate an {{site.data.keyword.cloud_notm}} API key:</strong> <a href="/docs/account?topic=account-userapikey#create_user_key">{{site.data.keyword.cloud_notm}} API keys</a> <img src="../icons/launch-glyph.svg" alt="External link icon"> are dependent on the {{site.data.keyword.cloud_notm}} account they are generated for. You cannot combine your {{site.data.keyword.cloud_notm}} API key with a different account ID in the same {{site.data.keyword.cloud_notm}} IAM token. To access clusters that were created with an account other than the one your {{site.data.keyword.cloud_notm}} API key is based on, you must log in to the account to generate a new API key.</li><li><strong>Use a one-time passcode: </strong> If you authenticate with {{site.data.keyword.cloud_notm}} by using a one-time passcode, you cannot fully automate the creation of your {{site.data.keyword.cloud_notm}} IAM token because the retrieval of your one-time passcode requires a manual interaction with your web browser. To fully automate the creation of your {{site.data.keyword.cloud_notm}} IAM token, you must create an {{site.data.keyword.cloud_notm}} API key instead.</ul>|
{: caption="ID types and options" caption-side="top"}
{: summary="ID types and options with the input parameter in column 1 and the value in column 2."}

1. Create your {{site.data.keyword.cloud_notm}} IAM access token. The body information that is included in your request varies based on the {{site.data.keyword.cloud_notm}} authentication method that you use.

    ```
    POST https://iam.cloud.ibm.com/identity/token
    ```
    {: codeblock}

    <table summary="Input parameters to retrieve IAM tokens with the input parameter in column 1 and the value in column 2.">
    <caption>Input parameters to get IAM tokens.</caption>
    <thead>
        <th>Input parameters</th>
        <th>Values</th>
    </thead>
    <tbody>
    <tr>
    <td>Header</td>
    <td><ul><li><code>Content-Type: application/x-www-form-urlencoded</code></li> <li>Authorization: Basic Yng6Yng=<p><strong>Note</strong>: <code>Yng6Yng=</code> equals the URL-encoded authorization for the username <strong>bx</strong> and the password <strong>bx</strong>.</p></li></ul>
    </td>
    </tr>
    <tr>
    <td>Body for {{site.data.keyword.cloud_notm}} username and password</td>
    <td><ul><li><code>grant_type: password</code></li>
    <li><code>response_type: cloud_iam uaa</code></li>
    <li><code>username</code>: Your {{site.data.keyword.cloud_notm}} username.</li>
    <li><code>password</code>: Your {{site.data.keyword.cloud_notm}} password.</li>
    <li><code>uaa_client_id: cf</code></li>
    <li><code>uaa_client_secret:</code></br><strong>Note</strong>: Add the <code>uaa_client_secret</code> key with no value specified.</li></ul></td>
    </tr>
    <tr>
    <td>Body for {{site.data.keyword.cloud_notm}} API keys</td>
    <td><ul><li><code>grant_type: urn:ibm:params:oauth:grant-type:apikey</code></li>
    <li><code>response_type: cloud_iam uaa</code></li>
    <li><code>apikey</code>: Your {{site.data.keyword.cloud_notm}} API key</li>
    <li><code>uaa_client_id: cf</code></li>
    <li><code>uaa_client_secret:</code> </br><strong>Note</strong>: Add the <code>uaa_client_secret</code> key with no value specified.</li></ul></td>
    </tr>
    <tr>
    <td>Body for {{site.data.keyword.cloud_notm}} one-time passcode</td>
        <td><ul><li><code>grant_type: urn:ibm:params:oauth:grant-type:passcode</code></li>
    <li><code>response_type: cloud_iam uaa</code></li>
    <li><code>passcode</code>: Your {{site.data.keyword.cloud_notm}} one-time passcode. Run <code>ibmcloud login --sso</code> and follow the instructions in your CLI output to retrieve your one-time passcode by using your web browser.</li>
    <li><code>uaa_client_id: cf</code></li>
    <li><code>uaa_client_secret:</code> </br><strong>Note</strong>: Add the <code>uaa_client_secret</code> key with no value specified.</li></ul>
    </td>
    </tr>
    </tbody>
    </table>

    Example output for using an API key:

    ```
    {
    "access_token": "<iam_access_token>",
    "refresh_token": "<iam_refresh_token>",
    "uaa_token": "<uaa_token>",
    "uaa_refresh_token": "<uaa_refresh_token>",
    "token_type": "Bearer",
    "expires_in": 3600,
    "expiration": 1493747503
    "scope": "ibm openid"
    }

    ```
    {: screen}

    You can find the {{site.data.keyword.cloud_notm}} IAM token in the **access_token** field of your API output. Note the {{site.data.keyword.cloud_notm}} IAM token to retrieve additional header information in the next steps.

2. Retrieve the ID of the {{site.data.keyword.cloud_notm}} account that you want to work with. Replace `<iam_access_token>` with the {{site.data.keyword.cloud_notm}} IAM token that you retrieved from the **access_token** field of your API output in the previous step. In your API output, you can find the ID of your {{site.data.keyword.cloud_notm}} account in the **resources.metadata.guid** field.

    ```sh
    GET https://accounts.cloud.ibm.com/coe/v2/accounts
    ```
    {: codeblock}

    <table summary="Input parameters to get {{site.data.keyword.cloud_notm}} account ID with the input parameter in column 1 and the value in column 2.">
    <caption>Input parameters to get an {{site.data.keyword.cloud_notm}} account ID.</caption>
    <thead>
        <th>Input parameters</th>
        <th>Values</th>
    </thead>
    <tbody>
        <tr>
          <td>Headers</td>
        <td><ul><li><code>Content-Type: application/json</code></li>
        <li><code>Authorization: bearer &lt;iam_access_token&gt;</code></li>
        <li><code>Accept: application/json</code></li></ul></td>
        </tr>
    </tbody>
    </table>

    Example output

    ```sh
    {
    "next_url": null,
    "total_results": 5,
    "resources": [
        {
            "metadata": {
                "guid": "<account_ID>",
                "url": "/coe/v2/accounts/<account_ID>",
                "created_at": "2016-09-29T02:49:41.842Z",
                "updated_at": "2018-08-16T18:56:00.442Z",
                "anonymousId": "1111a1aa1a1111a1aa11aa11111a1111"
            },
            "entity": {
                "name": "<account_name>",
    ```
    {: screen}

3. Generate a new {{site.data.keyword.cloud_notm}} IAM token that includes your {{site.data.keyword.cloud_notm}} credentials and the account ID that you want to work with.

    If you use an {{site.data.keyword.cloud_notm}} API key, you must use the {{site.data.keyword.cloud_notm}} account ID the API key was created for. To access clusters in other accounts, log into this account and create an {{site.data.keyword.cloud_notm}} API key that is based on this account.
    {: note}

    ```
    POST https://iam.cloud.ibm.com/identity/token
    ```
    {: codeblock}

    <table summary="Input parameters to retrieve IAM tokens with the input parameter in column 1 and the value in column 2.">
    <caption>Input parameters to get IAM tokens.</caption>
    <thead>
        <th>Input parameters</th>
        <th>Values</th>
    </thead>
    <tbody>
    <tr>
    <td>Header</td>
    <td><ul><li><code>Content-Type: application/x-www-form-urlencoded</code></li> <li><code>Authorization: Basic Yng6Yng=</code><p><strong>Note</strong>: <code>Yng6Yng=</code> equals the URL-encoded authorization for the username <strong>bx</strong> and the password <strong>bx</strong>.</p></li></ul>
    </td>
    </tr>
    <tr>
    <td>Body for {{site.data.keyword.cloud_notm}} username and password</td>
    <td><ul><li><code>grant_type: password</code></li>
    <li><code>response_type: cloud_iam uaa</code></li>
    <li><code>username</code>: Your {{site.data.keyword.cloud_notm}} username. </li>
    <li><code>password</code>: Your {{site.data.keyword.cloud_notm}} password. </li>
    <li><code>uaa_client_ID: cf</code></li>
    <li><code>uaa_client_secret:</code> </br><strong>Note</strong>: Add the <code>uaa_client_secret</code> key with no value specified.</li>
    <li><code>bss_account</code>: The {{site.data.keyword.cloud_notm}} account ID that you retrieved in the previous step.</li></ul>
    </td>
    </tr>
    <tr>
    <td>Body for {{site.data.keyword.cloud_notm}} API keys</td>
    <td><ul><li><code>grant_type: urn:ibm:params:oauth:grant-type:apikey</code></li>
    <li><code>response_type: cloud_iam uaa</code></li>
    <li><code>apikey</code>: Your {{site.data.keyword.cloud_notm}} API key.</li>
    <li><code>uaa_client_ID: cf</code></li>
    <li><code>uaa_client_secret:</code> </br><strong>Note</strong>: Add the <code>uaa_client_secret</code> key with no value specified.</li>
    <li><code>bss_account</code>: The {{site.data.keyword.cloud_notm}} account ID that you retrieved in the previous step.</li></ul>
        </td>
    </tr>
    <tr>
    <td>Body for {{site.data.keyword.cloud_notm}} one-time passcode</td>
    <td><ul><li><code>grant_type: urn:ibm:params:oauth:grant-type:passcode</code></li>
    <li><code>response_type: cloud_iam uaa</code></li>
    <li><code>passcode</code>: Your {{site.data.keyword.cloud_notm}} passcode. </li>
    <li><code>uaa_client_ID: cf</code></li>
    <li><code>uaa_client_secret:</code> </br><strong>Note</strong>: Add the <code>uaa_client_secret</code> key with no value specified.</li>
    <li><code>bss_account</code>: The {{site.data.keyword.cloud_notm}} account ID that you retrieved in the previous step.</li></ul></td>
    </tr>
    </tbody>
    </table>

    Example output

    ```json
    {
        "access_token": "<iam_token>",
        "refresh_token": "<iam_refresh_token>",
        "token_type": "Bearer",
        "expires_in": 3600,
        "expiration": 1493747503
    }

    ```
    {: screen}

    You can find the {{site.data.keyword.cloud_notm}} IAM token in the **access_token** and the refresh token in the **refresh_token** field of your API output.

4. List all classic or VPC clusters in your account.
    * **Classic**:
        ```sh
        GET https://containers.cloud.ibm.com/global/v2/classic/getClusters
        ```
        {: codeblock}

        <table summary="Input parameters to work with the {{site.data.keyword.openshiftlong_notm}} API with the input parameter in column 1 and the value in column 2.">
        <caption>Input parameters to work with the {{site.data.keyword.openshiftlong_notm}} API.</caption>
        <thead>
        <th>Input parameters</th>
        <th>Values</th>
        </thead>
        <tbody>
        <tr>
        <td>Header</td>
        <td><li><code>Authorization: bearer &lt;iam_token&gt;</code></td>
        </tr>
        </tbody>
        </table>
    * **VPC**:
        ```sh
        GET https://containers.cloud.ibm.com/global/v2/vpc/getClusters?provider=vpc-gen2
        ```
        {: codeblock}

        <table summary="Input parameters to work with the {{site.data.keyword.openshiftlong_notm}} API with the input parameter in column 1 and the value in column 2.">
        <caption>Input parameters to work with the {{site.data.keyword.openshiftlong_notm}} API.</caption>
        <thead>
        <th>Input parameters</th>
        <th>Values</th>
        </thead>
        <tbody>
        <tr>
        <td>Header</td>
        <td><code>Authorization</code>: Your {{site.data.keyword.cloud_notm}} IAM access token (<code>bearer &lt;iam_token&gt;</code>).</td>
        </tr>
        </tbody>
        </table>

5. Review the [{{site.data.keyword.openshiftlong_notm}} API documentation](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external} to find a list of supported APIs.

When you use the API for automation, be sure to rely on the responses from the API, not files within those responses. For example, the Kubernetes configuration file for your cluster context is subject to change, so do not build automation based on specific contents of this file when you use the `GET /v1/clusters/{idOrName}/config` call.
{: note}





## Refreshing {{site.data.keyword.cloud_notm}} IAM access tokens and obtaining new refresh tokens with the API
{: #cs_api_refresh}

Every {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) access token that is issued via the API expires after one hour. You must refresh your access token regularly to assure access to the {{site.data.keyword.cloud_notm}} API. You can use the same steps to obtain a new refresh token.
{: shortdesc}

Before you begin, make sure that you have an {{site.data.keyword.cloud_notm}} IAM refresh token or an {{site.data.keyword.cloud_notm}} API key that you can use to request a new access token.
- **Refresh token:** Follow the instructions in [Automating the cluster creation and management process with the {{site.data.keyword.cloud_notm}} API](#cs_api).
- **API key:** Retrieve your [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/) API key as follows.
    1. From the menu bar, click **Manage** > **Access (IAM)**.
    2. Click the **Users** page and then select yourself.
    3. In the **API keys** pane, click **Create an IBM Cloud API key**.
    4. Enter a **Name** and **Description** for your API key and click **Create**.
    5. Click **Show** to see the API key that was generated for you.
    6. Copy the API key so that you can use it to retrieve your new {{site.data.keyword.cloud_notm}} IAM access token.

Use the following steps if you want to create an {{site.data.keyword.cloud_notm}} IAM token or if you want to obtain a new refresh token.

1. Generate a new {{site.data.keyword.cloud_notm}} IAM access token by using the refresh token or the {{site.data.keyword.cloud_notm}} API key.
    ```
    POST https://iam.cloud.ibm.com/identity/token
    ```
    {: codeblock}

    <table summary="Input parameters for new IAM token with the input parameter in column 1 and the value in column 2.">
    <caption>Input parameters for a new {{site.data.keyword.cloud_notm}} IAM token</caption>
    <thead>
    <th>Input parameters</th>
    <th>Values</th>
    </thead>
    <tbody>
    <tr>
    <td>Header</td>
    <td><ul><li><code>Content-Type: application/x-www-form-urlencoded</code></li>
        <li><code>Authorization: Basic Yng6Yng=</code></br></br><strong>Note:</strong> <code>Yng6Yng=</code> equals the URL-encoded authorization for the username <strong>bx</strong> and the password <strong>bx</strong>.</li></ul></td>
    </tr>
    <tr>
    <td>Body when using the refresh token</td>
    <td><ul><li><code>grant_type: refresh_token</code></li>
    <li><code>response_type: cloud_iam uaa</code></li>
    <li><code>refresh_token:</code> Your {{site.data.keyword.cloud_notm}} IAM refresh token. </li>
    <li><code>uaa_client_ID: cf</code></li>
    <li><code>uaa_client_secret:</code></li>
    <li><code>bss_account:</code> Your {{site.data.keyword.cloud_notm}} account ID. </li></ul><strong>Note</strong>: Add the <code>uaa_client_secret</code> key with no value specified.</td>
    </tr>
    <tr>
        <td>Body when using the {{site.data.keyword.cloud_notm}} API key</td>
        <td><ul><li><code>grant_type: urn:ibm:params:oauth:grant-type:apikey</code></li>
    <li><code>response_type: cloud_iam uaa</code></li>
    <li><code>apikey:</code> Your {{site.data.keyword.cloud_notm}} API key. </li>
    <li><code>uaa_client_ID: cf</code></li>
        <li><code>uaa_client_secret:</code></li></ul><strong>Note:</strong> Add the <code>uaa_client_secret</code> key with no value specified.</td>
    </tr>
    </tbody>
    </table>

    Example API output:

    ```
    {
        "access_token": "<iam_token>",
        "refresh_token": "<iam_refresh_token>",
        "uaa_token": "<uaa_token>",
        "uaa_refresh_token": "<uaa_refresh_token>",
        "token_type": "Bearer",
        "expires_in": 3600,
        "expiration": 1493747503
    }

    ```
    {: screen}

    You can find your new {{site.data.keyword.cloud_notm}} IAM token in the **access_token**, and the refresh token in the **refresh_token** field of your API output.

2. Continue working with the [{{site.data.keyword.openshiftlong_notm}} API documentation](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external} by using the token from the previous step.



## Refreshing {{site.data.keyword.cloud_notm}} IAM access tokens and obtaining new refresh tokens with the CLI
{: #cs_cli_refresh}

You can use the command line to [set the cluster context](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure), download the `kubeconfig` file for your {{site.data.keyword.openshiftshort}} cluster, and generate an {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) ID token and a refresh token to provide authentication.
{: shortdesc}

You can use [{{site.data.keyword.cloud_notm}} IAM](https://cloud.ibm.com/iam/overview){: external} to change the default expiration times for your tokens and sessions.
{: tip}

**`Kubeconfig` session**: When you start a new CLI session or after the session expires such as after the default of 24 hours, you must reset the cluster context.

**ID token**: Every IAM ID token that is issued via the CLI expires after a set period of time, such as 20 minutes. When the ID token expires, the refresh token is sent to the token provider to refresh the ID token. Your authentication is refreshed, and you can continue to run commands against your cluster.

**Refresh token**: Refresh tokens expire after a set period of time, such as 30 days, or if the administrator revokes the token. If the refresh token is expired, the ID token cannot be refreshed, and you are not able to continue running commands in the CLI. You can get a new refresh token by running `ibmcloud oc cluster config --cluster <cluster_name>`. This command also refreshes your ID token.




