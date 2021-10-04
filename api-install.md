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

API endpoint prefix
:    v1 API: `https://containers.cloud.ibm.com/global/v1`
:    v2 API: `https://containers.cloud.ibm.com/global/v2`

API reference docs
:    v1 API: [`https://containers.cloud.ibm.com/global/swagger-global-api/`](https://containers.cloud.ibm.com/global/swagger-global-api/#/)
:    v2 API: [`https://containers.cloud.ibm.com/global/swagger-global-api/`](https://containers.cloud.ibm.com/global/swagger-global-api/#/).

API architectural style
:    v1 API: Representational state transfer (REST) that focuses on resources that you interact with through HTTP methods such as `GET`, `POST`, `PUT`, `PATCH`, and `DELETE`.
:    v2 API: Remote procedure calls (RPC) that focus on actions through only `GET` and `POST` HTTP methods.

Supported container platforms
:    v1 API: Use the {{site.data.keyword.openshiftlong_notm}} API to manage your {{site.data.keyword.cloud_notm}} infrastructure resources, such as worker nodes, for **both community Kubernetes and {{site.data.keyword.openshiftshort}} clusters**.
:    v2 API: Use the {{site.data.keyword.openshiftlong_notm}} `v2` API to manage your {{site.data.keyword.cloud_notm}} infrastructure resources, such as worker nodes, for **both community Kubernetes and {{site.data.keyword.openshiftshort}} VPC clusters**.

  
{{site.data.keyword.openshiftshort}} API
:    v1 API: To use the {{site.data.keyword.openshiftshort}} API to manage {{site.data.keyword.openshiftshort}} and Kubernetes resources within the cluster, such as pods or namespaces, you must log in by exchanging an {{site.data.keyword.cloud_notm}} API key for an {{site.data.keyword.openshiftshort}} access token. See [Using an API key to log in to clusters](/docs/openshift?topic=openshift-access_cluster#access_api_key).
:    v2 API: Same as `v1`; see [Using an API key to log in to clusters](/docs/openshift?topic=openshift-access_cluster#access_api_key).

Supported infrastructure providers
:    v1 API: `classic`
:    v2 API: `vpc` and `classic`
     - The `vpc` provider is designed to support multiple VPC subproviders. The supported VPC subprovider is `vpc-gen2`, which corresponds to a VPC cluster for Generation 2 compute resources.
     - Provider-specific requests have a path parameter in the URL, such as `v2/vpc/createCluster`. Some APIs are only available to a particular provider, such as `GET vlan` for classic or `GET vpcs` for VPC.
     - Provider-neutral requests can include a provider-specific body parameter that you specify, usually in JSON, such as `{"provider": "vpc"}`, if you want to return responses for only the specified provider.

`GET` responses
:    v1 API: The `GET` method for a collection of resources (such as `GET v1/clusters`) returns the same details for each resource in the list as a `GET` method for an individual resource (such as `GET v1/clusters/{idOrName}`).
:    v2 API: To return responses faster, the v2 `GET` method for a collection of resources (such as `GET v2/clusters`) returns only a subset of information that is detailed in a `GET` method for an individual resource (such as `GET v2/clusters/{idOrName}`).
     Some list responses include a providers property to identify whether the returned item applies to classic or VPC infrastructure. For example, the `GET zones` list returns some results such as `mon01` that are available only in the classic infrastructure provider, while other results such as `us-south-01` are available only in the VPC infrastructure provider.

Cluster, worker node, and worker-pool responses
:    v1 API: Responses include only information that is specific to the classic infrastructure provider, such as the VLANs in `GET` cluster and worker responses.
:    v2 API: The information that is returned varies depending on the infrastructure provider. For such provider-specific responses, you can specify the provider in your request. For example, VPC clusters do not return VLAN information since they do not have VLANs. Instead, they return subnet and CIDR network information.

## Automating cluster deployments with the API
{: #cs_api}

You can use the {{site.data.keyword.openshiftlong_notm}} API to automate the creation, deployment, and management of your {{site.data.keyword.openshiftshort}} clusters.
{: shortdesc}

The {{site.data.keyword.openshiftlong_notm}} API requires header information that you must provide in your API request and that can vary depending on the API that you want to use. To determine what header information is needed for your API, see the [{{site.data.keyword.openshiftlong_notm}} API documentation](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external}.

To authenticate with {{site.data.keyword.openshiftlong_notm}}, you must provide an {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) token that is generated with your {{site.data.keyword.cloud_notm}} credentials and that includes the {{site.data.keyword.cloud_notm}} account ID where the cluster was created. Depending on the way you authenticate with {{site.data.keyword.cloud_notm}}, you can choose between the following options to automate the creation of your {{site.data.keyword.cloud_notm}} IAM token.

You can also use the [API swagger JSON file](https://containers.cloud.ibm.com/global/swagger-global-api/swagger.json){: external} to generate a client that can interact with the API as part of your automation work.
{: tip}

Unfederated ID
:    - **Generate an {{site.data.keyword.cloud_notm}} API key:** As an alternative to using the {{site.data.keyword.cloud_notm}} username and password, you can [use {{site.data.keyword.cloud_notm}} API keys](/docs/account?topic=account-userapikey#create_user_key). {{site.data.keyword.cloud_notm}} API keys are dependent on the {{site.data.keyword.cloud_notm}} account they are generated for. You cannot combine your {{site.data.keyword.cloud_notm}} API key with a different account ID in the same {{site.data.keyword.cloud_notm}} IAM token. To access clusters that were created with an account other than the one your {{site.data.keyword.cloud_notm}} API key is based on, you must log in to the account to generate a new API key.
     - **{{site.data.keyword.cloud_notm}} username and password:** You can follow the steps in this topic to fully automate the creation of your {{site.data.keyword.cloud_notm}} IAM access token.
     
Federated ID
:    - **Generate an {{site.data.keyword.cloud_notm}} API key:** [{{site.data.keyword.cloud_notm}} API keys](/docs/account?topic=account-userapikey#create_user_key) are dependent on the {{site.data.keyword.cloud_notm}} account they are generated for. You cannot combine your {{site.data.keyword.cloud_notm}} API key with a different account ID in the same {{site.data.keyword.cloud_notm}} IAM token. To access clusters that were created with an account other than the one your {{site.data.keyword.cloud_notm}} API key is based on, you must log in to the account to generate a new API key.
     - **Use a one-time passcode:** If you authenticate with {{site.data.keyword.cloud_notm}} by using a one-time passcode, you cannot fully automate the creation of your {{site.data.keyword.cloud_notm}} IAM token because the retrieval of your one-time passcode requires a manual interaction with your web browser. To fully automate the creation of your {{site.data.keyword.cloud_notm}} IAM token, you must create an {{site.data.keyword.cloud_notm}} API key instead.


1. Create your {{site.data.keyword.cloud_notm}} IAM access token. The body information that is included in your request varies based on the {{site.data.keyword.cloud_notm}} authentication method that you use.

    ```sh
    POST https://iam.cloud.ibm.com/identity/token
    ```
    {: codeblock}
    
    Header 
    :    - `Content-Type: application/x-www-form-urlencoded` 
         - Authorization: Basic `Yng6Yng=`
             `Yng6Yng=` equals the URL-encoded authorization for the username **bx** and the password **bx**.
             {: note}
         
    Body for {{site.data.keyword.cloud_notm}} username and password
    :    - `grant_type: password` 
         - `response_type: cloud_iam uaa`
         - `username`: Your {{site.data.keyword.cloud_notm}} username.
         - `password`: Your {{site.data.keyword.cloud_notm}} password. 
         - `uaa_client_id: cf`
         - `uaa_client_secret:`
             Add the `uaa_client_secret` key with no value specified.
             {: note}
         
    Body for {{site.data.keyword.cloud_notm}} API keys 
    :    - `grant_type: urn:ibm:params:oauth:grant-type:apikey` 
         - `response_type: cloud_iam uaa` 
         - `apikey`: Your {{site.data.keyword.cloud_notm}} API key 
         - `uaa_client_id: cf`
         - `uaa_client_secret:`
             Add the `uaa_client_secret` key with no value specified.
             {: note}
         
    Body for {{site.data.keyword.cloud_notm}} one-time passcode
    :    - `grant_type: urn:ibm:params:oauth:grant-type:passcode` 
         - `response_type: cloud_iam uaa` 
         - `passcode`: Your {{site.data.keyword.cloud_notm}} one-time passcode. Run `ibmcloud login --sso` and follow the instructions in your CLI output to retrieve your one-time passcode by using your web browser. 
         - `uaa_client_id: cf` 
         - `uaa_client_secret:`
             Add the `uaa_client_secret` key with no value specified.
             {: note}

    The following example shows output for the previous request.

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
    
    Header
    :    - `Content-Type: application/json`
         - `Authorization: bearer <iam_access_token>`
         - `Accept: application/json`

    The following example shows the output of the previous request.

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

    ```sh
    POST https://iam.cloud.ibm.com/identity/token
    ```
    {: codeblock}
    
    Header
    :    - `Content-Type: application/x-www-form-urlencoded`
         - `Authorization: Basic Yng6Yng=`
             `Yng6Yng=` equals the URL-encoded authorization for the username **bx** and the password **bx**.
             {: note}
         
    Body for {{site.data.keyword.cloud_notm}} username and password
    :    - `grant_type: password`
         - `response_type: cloud_iam uaa`
         - `username`: Your {{site.data.keyword.cloud_notm}} username.
         - `password`: Your {{site.data.keyword.cloud_notm}} password.
         - `uaa_client_ID: cf`
         - `uaa_client_secret:`
             Add the `uaa_client_secret` key with no value specified.
             {: note}
         - `bss_account`: The {{site.data.keyword.cloud_notm}} account ID that you retrieved in the previous step.
         
    Body for {{site.data.keyword.cloud_notm}} API keys
    :    - `grant_type: urn:ibm:params:oauth:grant-type:apikey`
         - `response_type: cloud_iam uaa` 
         - `apikey`: Your {{site.data.keyword.cloud_notm}} API key. 
         - `uaa_client_ID: cf` \n - `uaa_client_secret:`
             Add the `uaa_client_secret` key with no value specified.
             {: note}
         - `bss_account`: The {{site.data.keyword.cloud_notm}} account ID that you retrieved in the previous step.
         
    Body for {{site.data.keyword.cloud_notm}} one-time passcode
    :    - `grant_type: urn:ibm:params:oauth:grant-type:passcode` \n 
    - `response_type: cloud_iam uaa` \n - `passcode`: Your {{site.data.keyword.cloud_notm}} passcode. \n - `uaa_client_ID: cf` \n - `uaa_client_secret:` \n - `bss_account`: The {{site.data.keyword.cloud_notm}} account ID that you retrieved in the previous step. \n **Note**: Add the `uaa_client_secret` key with no value specified.
    {: caption="Table 2. Input parameters for API request." caption-side="top"}

    The following example shows output for the API request.

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
    * **Classic**
    
        ```sh
        GET https://containers.cloud.ibm.com/global/v2/classic/getClusters
        ```
        {: codeblock}

        Header
        :     `Authorization: bearer <iam_token>`

    * **VPC**
    
        ```sh
        GET https://containers.cloud.ibm.com/global/v2/vpc/getClusters?provider=vpc-gen2
        ```
        {: codeblock}

        Header
        :     `Authorization`: Your {{site.data.keyword.cloud_notm}} IAM access token (`bearer <iam_token>`).

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
    ```sh
    POST https://iam.cloud.ibm.com/identity/token
    ```
    {: codeblock}

    Header
    :     - `Content-Type: application/x-www-form-urlencoded`
          - `Authorization: Basic Yng6Yng=`
              `Yng6Yng=` equals the URL-encoded authorization for the username **bx** and the password **bx**.
              {: note}
    
    Body when using the refresh token
    :     - `grant_type: refresh_token`
          - `response_type: cloud_iam uaa`
          - `refresh_token:` Your {{site.data.keyword.cloud_notm}} IAM refresh token.
          - `uaa_client_ID: cf`
          - `uaa_client_secret:`
          - `bss_account:` Your {{site.data.keyword.cloud_notm}} account ID.
              Add the `uaa_client_secret` key with no value specified.
              {: note}
          
    Body when using the {{site.data.keyword.cloud_notm}} API key
    :     - `grant_type: urn:ibm:params:oauth:grant-type:apikey`
          - `response_type: cloud_iam uaa`
          - `apikey:` Your {{site.data.keyword.cloud_notm}} API key.
          - `uaa_client_ID: cf`
          - `uaa_client_secret:`
              Add the `uaa_client_secret` key with no value specified.
              {: note}

    The following example shows the output of the previous API request.

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

`Kubeconfig` session
:    When you start a new CLI session or after the session expires such as after the default of 24 hours, you must reset the cluster context.

ID token
:    Every IAM ID token that is issued via the CLI expires after a set period of time, such as 20 minutes. When the ID token expires, the refresh token is sent to the token provider to refresh the ID token. Your authentication is refreshed, and you can continue to run commands against your cluster.

Refresh token
:    Refresh tokens expire after a set period of time, such as 30 days, or if the administrator revokes the token. If the refresh token is expired, the ID token cannot be refreshed, and you are not able to continue running commands in the CLI. You can get a new refresh token by running `ibmcloud oc cluster config --cluster <cluster_name>`. This command also refreshes your ID token.
