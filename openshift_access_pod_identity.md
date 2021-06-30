---

copyright:
  years: 2014, 2021
lastupdated: "2021-06-30"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
  
  

# Authorizing pods in your cluster to {{site.data.keyword.cloud_notm}} services with IAM trusted profiles
{: #pod-iam-identity}

Give application pods that run in your {{site.data.keyword.openshiftlong}} cluster access to {{site.data.keyword.cloud_notm}} services by creating a trusted profile in {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).  
{: shortdesc}

Authorizing pods with IAM trusted profiles is available for new clusters that run {{site.data.keyword.openshiftshort}} version 4.7 or later.
{: note}

**In IAM**: Start by creating an IAM trusted profile, and assigning access policies or adding the trusted profile to an access group with the access policies. Then, you link the trusted profile with a Kubernetes namespace in your cluster. 

**In your cluster**: Through [Kubernetes service account token volume projection](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#service-account-token-volume-projection){: external}, the apps that run in your linked cluster's namespace and use the namespace's service account can exchange the cluster's public key to get an {{site.data.keyword.cloud_notm}} IAM access token. Your app can use this access token to authenticate API requests to {{site.data.keyword.cloud_notm}} services, such as databases, {{site.data.keyword.watson}}, or VPC infrastructure. Through the access policies of the trusted profile, you control what actions the token lets the app perform.

## Prerequisites
{: #iam-identity-prereqs}

To use {{site.data.keyword.cloud_notm}} IAM identities for pods in your cluster, verify that you meet the prerequisites.
{: shortdesc}

**Supported infrastructure provider**:
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

**Minimum required permissions**: 
* **Viewer** [platform](/docs/openshift?topic=openshift-access_reference#iam_platform) access role and the **Writer** [service](/docs/openshift?topic=openshift-access_reference#service) access role for the cluster in {{site.data.keyword.cloud_notm}} IAM for **{{site.data.keyword.containershort}}**.
* The `iam-identity.profile.create` and `iam-identity.profile.linkToResource` actions for the [IAM identity service](/docs/account?topic=account-iam-service-roles-actions#iam-identity-service).

**Supported version**: The cluster must be [created](/docs/openshift?topic=openshift-clusters) at {{site.data.keyword.openshiftshort}} version 4.7 or later. You cannot use a cluster that was updated to this version from a previous version.

**Log in to the cluster**: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

## Creating an IAM trusted profile for your cluster in the API
{: #iam-identity-create-api}
{: api}

**Before you begin**: Verify that you meet the [prerequisites](#iam-identity-prereqs).

1.  Create an IAM trusted profile in {{site.data.keyword.cloud_notm}} Identity and Access Management. Note the `uuid` (profile ID) in the output.

    *   Replace `<access_token>` with your {{site.data.keyword.cloud_notm}} token. To get this token from the command line, log in and run `ibmcloud iam oauth-tokens`.
    *   Enter a `<profile_name>` and optional `<description>` for the IAM trusted profile.
    *   Replace `<account_id>` with the ID of your {{site.data.keyword.cloud_notm}} account. To get this ID from the command line, run `ibmcloud account show`.

    ```
    curl -L -X POST 'https://iam.cloud.ibm.com/v1/profiles' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer <access_token>' \
    -H 'Content-Type: application/json' \
    --data-raw '{
        "name": "<profile_name>",
        "description": "<description>",
        "account_id": "<account_id>"
    }'
    ```
    {: codeblock}

2.  [Assign the trusted profile to an access group](/docs/account?topic=account-groups#access_ag_api) with access policies to the {{site.data.keyword.cloud_notm}} services that you want your apps to have access to.
3.  Link the IAM trusted profile to a Kubernetes namespace in your {{site.data.keyword.openshiftlong_notm}} cluster.
    1.  Get your `<profile-id>` from the output of the first step. Or, you can run the following API command.
        ```
        curl -L -X GET 'https://iam.cloud.ibm.com/v1/profiles/?account_id=<account_id>' \
        -H 'Accept: application/json' \
        -H 'Authorization: <access_token>' \
        -H 'Content-Type: application/json' \
        ```
        {: codeblock}
    2.  Get your cluster name and CRN by running the following API command.
        ```
        curl --location --request GET 'https://containers.cloud.ibm.com/global/v1/clusters' \
        --header 'Authorization: <access_token>'
        ```
        {: codeblock}
    3.  Link the IAM trusted profile to your cluster.

        * For `<link_name>`, enter a name for the link between the trusted profile and the cluster.
        * Replace `<profile-id>`, `<access_token>`, `<cluster_crn>`, and `<cluster_name>` with the values that you previously retrieved.
        * For `<ns>`, enter the namespace in your cluster. You can list namespaces by logging in to the cluster and running `oc get ns`.

        ```
        curl -L -X POST 'https://iam.cloud.ibm.com/v1/profiles/<profile-id>/links' \
        -H 'Accept: application/json' \
        -H 'Authorization: Bearer <access_token>' \
        -H 'Content-Type: application/json' \
        --data-raw '{
            "name": "<link_name>",
            "cr_type": "ROKS_SA",
            "link": {
                "crn": "<cluster_crn>",
                "namespace": "<ns>",
                "name": "<cluster_name>"
            }
        }'
        ```
        {: codeblock}
        
4.  When you [design your pod configuration file](/docs/openshift?topic=openshift-openshift_apps), mount the identity token in the `volumeMounts` of the `containers` section.
    ```
    ...
        volumeMounts:
        - mountPath: /var/run/secrets/tokens
          name: vault-token
    ```
    {: codeblock}
5.  Use the token to authenticate to IAM for subsequent API calls. For example, the following job deploys a `curl` pod that makes an API request to {{site.data.keyword.cloud_notm}} IAM to verify that the cluster's public key is exchanged for an IAM access token. Your app might call other {{site.data.keyword.cloud_notm}} services that the trusted profile authorizes.
    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
      name: token-exchange-job
      namespace: default
    spec:
      template:
        spec:
          containers:
          - name: curl
            image: curlimages/curl:7.77.0
            command: ["/bin/sh"]
            args: ["-c", "curl -s -H \"Content-Type: application/x-www-form-urlencoded\" -H \"Accept: application/json\" -d grant_type=urn:ibm:params:oauth:grant-type:cr-token -d cr_token=$(cat /var/run/secrets/tokens/vault-token) -d profile_id==<profile_id> https://iam.cloud.ibm.com/identity/token"]
            volumeMounts:
            - mountPath: /var/run/secrets/tokens
              name: vault-token
          restartPolicy: Never
          serviceAccountName: default
          volumes:
          - name: vault-token
            projected:
              sources:
              - serviceAccountToken:
                  path: vault-token
                  expirationSeconds: 7200
                  audience: vault
    ```
    {: codeblock}
5.  Check the logs of your pod to verify that the call is successful.
    ```
    oc logs <pod>
    ```
    {: pre}

<br />


