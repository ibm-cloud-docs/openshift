---

copyright: 
  years: 2025, 2025
lastupdated: "2025-08-12"


keywords: trusted profiles, containers, block storage, openshift
subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Configuring a trusted profile for cluster components
{: #configure-trusted-profile}

You can use trusted profiles to control access to your resources, including components such as Block Storage, File Storage, or Cloud Object Storage.
{: shortdesc} 

## About trusted profiles
{: #tp-about}

By using trusted profiles, you can establish a flexible, secure way for federated users to access the IBM Cloud resources in your account. All federated users that share certain attributes defined in your corporate user directory are mapped to a common profile and can share access to IBM Cloud resources. This common identity makes it possible to give the members of your organization that share access requirements automatic access to resources one time, rather than having to add each user to an account and then grant them access directly or by using access groups.

Benefits of trusted profiles include:

Eliminating the need for long-lived API keys
:   Grant access to your resources based on a trusted relationship that you establish when you create the trusted profile rather than embedded API keys. This reduces the risk of compromised or leaked credentials. 

Centralized access control
:   Manage permissions through a single trusted profile for a simplified process of granting, revoking, or auditing access. 

Scoped permissions
:   Adhere to the principle of least privilege by creating profiles with the exact minimum permissions required to complete a specific task.


## Minimum access requirements
{: #tp-minreqs}

A minimum set of access policies are required for a trusted profile to be used for your storage components. 

### Minimum requirements for all storage components
{: #tp-minreqs-all}

Create a trust relationship with the following configuration. These permissions are required for VPC clusters. 
- Compute service type (found under the **Compute resource tab** in the UI) :
    - `Kubernetes`
    - `Red Hat OpenShift`
- Trusted namespace: `kube-system`.

Create access policies with the permissions in the following table.

| Service name |  Required permission | Description |
| ------------ | ------------------- | ---- |
| Billing  |  **Editor** | Editor | Allows viewing and managing billing data such as usage, cost, and reports. Useful for automated cost tracking or budget-aware operations. |
| Kubernetes service  | **Administrator**  | Enables Kubernetes clusters to interact with storage resources. |
| VPC Infrastructure service  |  **Writer, Editor** | Writer, Editor | Enables provisioning and management of storage resources. |
| Resource group | **Viewer** | Specify the resource group where the trusted profile is applied. For operations across multiple resource groups, you must specify all relevant resource groups. Note that if you are creating a custom storage class with the resource group, you must also assign **Viewer** access to the trusted profile for the resource group.
{: caption="Minimum permissions for all storage components" caption-side="bottom"}

Additionally, if you plan to use **Classic infrastructure** you must enable the **Add/Upgrade Storage (Storage Layer)** permission. To enable this permission, navigate to the [Trusted profile dashboard](https://cloud.ibm.com/iam/trusted-profiles){: external} in the UI and select the relevant trusted profile. Click **Classic infrastructure**, then expand the options under **Sales** to find the permission. 


### Minimum requirements for individual storage components
{: #tp-minreqs-component}

### VPC block storage
{: #tp-minreqs-vpc-block}

Create a trust relationship with the following configuration.
- Compute service type (found under the **Compute resource tab** in the UI) :
    - `Kubernetes`
    - `Red Hat OpenShift`
- Trusted namespace: `kube-system`.

Create access policies with the permissions in the following table.

| Service name | Required permission | Description |
| ------------ | ------------------- | ----------- |
| Kubernetes service  |  **Operator** | Enables Kubernetes clusters to interact with block storage resources. |
| VPC Infrastructure service  | **Writer, Editor, Snapshot Remote Account Restorer** | Enables provisioning, management, and cross snapshot operations for block storage resources. | 
| Resource group | **Viewer** | Specify the resource group where the trusted profile is applied. For operations across multiple resource groups, you must specify all relevant resource groups. Note that if you are creating a custom storage class with the resource group, you must also assign **Viewer** access to the trusted profile for the resource group.  |
{: caption="Minimum permissions for VPC block" caption-side="bottom"}

### Classic block storage
{: #tp-minreqs-classic-block}

Create a trust relationship with the following configuration.
- Compute service type (found under the **Compute resource tab** in the UI) :
    - `Kubernetes`
    - `Red Hat OpenShift`
- Trusted namespace: `kube-system`.

Add the permissions in the following table. To enable these permissions, you must use the UI. Navigate to the [Trusted profile dashboard](https://cloud.ibm.com/iam/trusted-profiles){: external} in the UI and select the relevant trusted profile. Click **Classic infrastructure**, then expand the options to find the permissions. 

| Service name | Required permission | Description |
| ------------ | ------------------- | ----------- |
| `Devices` | **Storage Manage**  |  Enables attachment, detachment, and configuration of Classic block storage on devices.  |
| `Sales` | **Add/Upgrade Storage(Storage Layer)** | Grants permission to order, upgrade, or modify Classic storage offerings via the Sales APIs. |
{: caption="Minimum permissions for Classic Block" caption-side="bottom"}

Compute service type  in compute resource  tab instead of Compute resources

### VPC file storage
{: #tp-minreqs-vpc-file}

Create a trust relationship with the following configuration.
- Compute service type (found under the **Compute resource tab** in the UI) :
    - `Kubernetes`
    - `Red Hat OpenShift`
- Trusted namespace: `kube-system`.

Create access policies with the permissions in the following table.

| Service name | Required permission | Description |
| ------------ | ------------------- | ----------- |
| Kubernetes service  |  **Operator** | Enables Kubernetes clusters to interact with file storage resources. |
| VPC Infrastructure service  | **Writer, Editor** | Enables provisioning and management of file storage resources. |
| Resource group | **Viewer** | Specify the resource group where the trusted profile is applied. For operations across multiple resource groups, you must specify all relevant resource groups. Note that if you are creating a custom storage class with the resource group, you must also assign **Viewer** access to the trusted profile for the resource group.  |
{: caption="Minimum permissions for VPC File storage" caption-side="bottom"}

### Classic file storage
{: #tp-minreqs-classic-file}

Create a trust relationship with the following configuration.
- Compute service type (found under the **Compute resource tab** in the UI) :
    - `Kubernetes`
    - `Red Hat OpenShift`
- Trusted namespace: `kube-system`.

Add the permissions in the following table. To enable these permissions, you must use the UI. Navigate to the [Trusted profile dashboard](https://cloud.ibm.com/iam/trusted-profiles){: external} in the UI and select the relevant trusted profile. Click **Classic infrastructure**, then expand the options to find the permissions. 

| Service name | Required permission | Description |
| ------------ | ------------------- | ----------- |
| `Devices` | **Storage Manage**  |  Enables attachment, detachment, and configuration of Classic block storage on devices.  |
| `Sales` | **Add/Upgrade Storage(Storage Layer)** | Grants permission to order, upgrade, or modify Classic storage offerings via the Sales APIs. |
{: caption="Minimum permissions for Classic File storage" caption-side="bottom"}


### Cluster autoscaler
{: #tp-minreqs-autoscaler}

Create a trust relationship with the following configuration.
- Compute service type (found under the **Compute resource tab** in the UI) :
    - `Kubernetes`
    - `Red Hat OpenShift`
- Trusted namespace: `kube-system`.

Create access policies with the permissions in the following table.

| Service name | Required permission | Description |
| ------------ | ------------------- | ----------- |
| Kubernetes service   | **Administrator**  | Enables Kubernetes clusters to interact with auto-scaler components. |
{: caption="Minimum permissions for cluster autoscaler" caption-side="bottom"}

### Object Storage
{: #tp-minreqs-cos}

Create a trust relationship with the following configuration.
- Compute service type (found under the **Compute resource tab** in the UI) :
    - `Kubernetes`
    - `Red Hat OpenShift`
- Trusted namespace: `kube-system`.

Create access policies with the permissions in the following table.

| Service name | Required permission | Description |
| ------------ | ------------------- | ----------- |
| Kubernetes service  |  **Reader, Viewer** | Enables Kubernetes clusters to interact with the COS plug-in. |
| VPC Infrastructure service  | **Reader, Viewer** | Enables the communication with VPC to get API calls.  |
| Resource group | **Viewer** | Specify the resource group where the trusted profile is applied. For operations across multiple resource groups, you must specify all relevant resource groups. |
{: caption="Minimum permissions for Object storage" caption-side="bottom"}

### ODF billing agent
{: #tp-minreqs-odf-billing}

Create a trust relationship with the following configuration.
- Compute service type (found under the **Compute resource tab** in the UI) :
    - `Kubernetes`
    - `Red Hat OpenShift`
- Trusted namespace: `kube-system`.

Create access policies with the permissions in the following table.

| Service name | Required permission | Description |
| ------------ | ------------------- | ----------- |
| `billing` | **Editor**  | Billing service. Allows viewing and managing billing data such as usage, cost, and reports. Useful for automated cost tracking or budget-aware operations. |
| Kubernetes service  | **Editor** | Enables Kubernetes clusters to interact with block storage. |
| VPC Infrastructure service  | **Editor, Writer** | Allows provisioning and management of storage resources. |
| Resource group | **Viewer** | Specify the resource group where the trusted profile is applied. For operations across multiple resource groups, you must specify all relevant resource groups. |
{: caption="Minimum permissions for ODF" caption-side="bottom"}


## Set up a trusted profile in the CLI
{: #tp-setup-cli}
{: cli}

Follow the steps to create and set up a trusted profile in the CLI.

Once you add a trusted profile to a cluster, it cannot be removed and you cannot resume using an API key for your resources. Make sure you follow these steps carefully to ensure that your trusted profile is set up correctly. 
{: important}

1. Log in to the IBM Cloud CLI. 
    ```sh
    ibmcloud login --apikey <API_KEY> -g <RESOURCE_GROUP>
    ```
    {: pre}

2. Run the command to create a trusted profile. For a complete list of command options, see the [IAM CLI docs](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_create).
    ```sh
    ibmcloud iam trusted-profile-create NAME --description "Identity for storage"
    ```
    {: pre}

3. Attach a rule to scope usage to the `kube‑system` namespace. For a complete list of command options, see the [IAM CLI docs](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_rule_create). 
    ```sh
    ibmcloud iam trusted-profile-rule-create --name NAME --type Profile-CR --cr-type ROKS_SA  --conditions claim:namespace,operator:EQUALS,value:kube-system 
    ```
    {: pre}

4. **For VPC clusters**: Create and assign access policies to the trusted profile. This example assigns the minimum permissions required for all storage components. For a list of permissions required for individual components only, see [Minimum requirements for individual storage components](#tp-minreqs-component). Specify the name or ID of the trusted profile you want to assign the policy to. For a complete list of command options, see the [IAM CLI docs](/docs/account?topic=account-ibmcloud_commands_iam#ibmcloud_iam_trusted_profile_policy_create). This step does not apply to classic clusters. 
    Add policies for the VPC Infrastructure service. 

    ```sh
    ibmcloud iam trusted-profile-policy-create NAME|ID  --roles Editor,Writer --service-name is
    ```
    {: pre}

    Add policies for the billing service. 

    ```sh
    ibmcloud iam trusted-profile-policy-create NAME|ID --roles Editor --service-name billing
    ```
    {: pre}

    Add policies for the Kubernetes service. 
    ```sh
    ibmcloud iam trusted-profile-policy-create NAME|ID --roles Administrator --service-name "containers-kubernetes"
    ```
    {: pre}

    Add policies for the relevant resource group that the trusted profile is applied to. Specify the resource group that the trusted profile is applied to. 

    ```sh
    ibmcloud iam trusted-profile-policy-create NAME|ID --roles Operator  --resource-type "resource-group" --resource "my-resource-group"
    ```
    {: pre}

4. **For classic clusters**: Add permissions to the trusted profile by using the UI. 
    1. Log in to your IBM Cloud account and navigate to the Trusted Profiles page. 
    1. Click the trusted profile you just created.
    2. Navigate to the **Classic Infrastructure** tab.
    3. In the permissions drop down, select the required permissions to meet the [minimum requirements](#tp-minreqs) for the relevant components. 

5. After you have created the trusted profile and assigned the required access policies, [set the trusted profile](#tp-set-cluster-rg) for either the cluster or the resource group that your clusters are in. Setting the trusted profile applies it to your storage components. 

## Set up a trusted profile with the UI
{: #tp-setup-ui}
{: ui}

Follow the steps to create and set up a trusted profile in the CLI.

Once you add a trusted profile to a cluster, it cannot be removed and you cannot resume using an API key for your resources. Make sure you follow these steps carefully to ensure that your trusted profile is set up correctly. 
{: important}

1. Log in to your IBM Cloud account and navigate to the Trusted Profiles page. 

2. Create a trusted profile. 

3. Create a trust relationship with the {{site.data.keyword.openshiftlong_notm}} service. 
    1. In the **Select trusted entity type** section, click **Compute resources**.
    2. Under **Create trust relationship**, choose **Red Hat OpenShift**.
    3. Select **All service resources**. Then add a condition to allow access when **Namespace** is **Equal** to `kube-system`. 
        - Note: You can instead choose specific resources that exist in your account. 

4. Click **Create**.

5. **VPC only**. Add access policies to the trusted profile. 
    1. From the **Trusted profiles** page, click the trusted profile you just created. 
    2. From the **Access** tab, click **Assign access**.
    3. In the **How do you want to assign access?** section, click **Access policy**.
    4. Add the services and roles to meet the [minimum requirements](#tp-minreqs) for the relevant components. Apply the policy to all resources. 

6. **Classic only**. Add permissions to the trusted profile. 
    1. From the **Trusted profiles** page, click the trusted profile you just created.
    2. Navigate to the **Classic Infrastructure** tab.
    3. In the permissions drop down, select the required permissions to meet the [minimum requirements](#tp-minreqs) for the relevant components. 


## Set up a trusted profile with the API
{: #tp-setup-api}
{: api}

1. Create a trusted profile.

    ```sh
    curl --request POST \
    --url https://iam.test.cloud.ibm.com/v1/profiles \
    --header 'Content-Type: application/json' \
    --data '{
        "name":"<PROFILE_NAME>",
        "account_id":"<ACCOUNT_ID>"
    }'
    ```
    {: pre}

2. Attach a rule to scope usage to the `kube‑system` namespace.

    ```sh
    curl --request POST \
    --url https://iam.test.cloud.ibm.com/v1/profiles/<PROFILE_NAME>/rules \
    --header 'Content-Type: application/json' \
    --data '{
        "type": "Profile-CR",
        "cr_type":"ROKS_SA",
        "conditions": [
            {
                "claim": "namespace",
                "operator": "EQUALS",
                "value": "\"kube-system\""
            }
        ]
    }'
    ```
    {: pre}
	
3. **For VPC clusters**: Attach access policies to VPC components. These examples assign the minimum permissions required for all storage components.  
       
    ```curl
    curl --request POST \
    --url https://iam.test.cloud.ibm.com/v1/policies \
    --header 'Content-Type: application/json' \
    --data '{
        "type": "access",
        "description": "Writer, Operator role for VPC infrastructure services",
        "subjects": [
            {
                "attributes": [
                    {
                        "name": "iam_id",
                        "value": "<IAM_PROFILE>"
                    }
                ]
            }
        ],
        "roles": [
            {
                "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Writer"
            },
            {
                "role_id": "crn:v1:bluemix:public:iam::::role:Editor"
            }
        ],
        "resources": [
            {
                "attributes": [
                    {
                        "name": "accountId",
                        "value": "<ACCOUNT_ID>"
                    },
                    {
                        "name": "serviceName",
                        "value": "is"
                    }
                ]
            }
        ]
    }'
    ```
    {: codeblock}

    ```curl
    curl --request POST \
    --url https://iam.test.cloud.ibm.com/v1/policies \
    --header 'Content-Type: application/json' \
    --data '{
        "type": "access",
        "description": "Editor role for billing services",
        "subjects": [
            {
                "attributes": [
                    {
                        "name": "iam_id",
                        "value": "<IAM_PROFILE>"
                    }
                ]
            }
        ],
        "roles": [
            {
                "role_id": "crn:v1:bluemix:public:iam::::role:Editor"
            }
        ],
        "resources": [
            {
                "attributes": [
                    {
                        "name": "accountId",
                        "value": "<ACCOUNT_ID>"
                    },
                    {
                        "name": "serviceName",
                        "value": "billing"
                    }
                ]
            }
        ]
    }'
    ```
    {: codeblock}

    ```curl
    curl --request POST \
    --url https://iam.test.cloud.ibm.com/v1/policies \
    --header 'Content-Type: application/json' \
    --data '{	
        "type": "access",
        "description": "Administrator role for containers-kubernetes services",
        "subjects": [
            {
                "attributes": [
                    {
                        "name": "iam_id",
                        "value": "<IAM_PROFILE>"
                    }
                ]
            }
        ],
        "roles": [
            {
                "role_id": "crn:v1:bluemix:public:iam::::role:Administrator"
            }
        ],
        "resources": [
            {
                "attributes": [
                    {
                        "name": "accountId",
                        "value": "<ACCOUNT_ID>"
                    },
                    {
                        "name": "serviceName",
                        "value": "containers-kubernetes"
                    }
                ]
            }
        ]
    }'
    {: codeblock}
        
    ```curl
    curl --request POST \
    --url https://iam.test.cloud.ibm.com/v1/policies \
    --header 'Content-Type: application/json' \
    --data '{	
        "type": "access",
        "subjects": [
            {
                "attributes": [
                    {
                        "name": "iam_id",
                        "value": "<IAM_PROFILE>"
                    }
                ]
            }
        ],
        "roles": [
            {
                "role_id": "crn:v1:bluemix:public:iam::::role:Operator"
            }
        ],
        "resources": [
            {
                "attributes": [
                    {
                        "name": "accountId",
                        "value": "<ACCOUNT_ID>"
                    },
                    {
                        "name": "resource",
                        "value": "<RESOURCE_GROUP_ID>"
                    },
                    {
                        "name": "resourceType",
                        "value": "resource-group"
                    },
                ]
            }
        ]
    }
    ```
    {: codeblock}

4. **For classic clusters**: Add permissions to the trusted profile by using the UI. 
    1. Log in to your IBM Cloud account and navigate to the Trusted Profiles page. 
    2. Click the trusted profile you just created.
    3. Navigate to the **Classic Infrastructure** tab.
    4. In the permissions drop down, select the required permissions to meet the [minimum requirements](#tp-minreqs) for the relevant components. 



## Setting the trusted profile for a cluster or resource group
{: #tp-set-cluster-rg}

When you set a trusted profile for your cluster, it applies to your storage components. You can set a trusted profile for an individual cluster, or to a resource group. 

Once you add a trusted profile to a cluster, it cannot be removed and you cannot resume using an API key for your resources. Make sure you follow these steps carefully to ensure that your trusted profile is set up correctly. 
{: important}

1. Make sure you have created a trusted profile that meets the [minimum requirements for storage components](#tp-minreqs). 

2. Assign the trusted profile to your cluster, or to the resource group that your cluster is in. If you assign a trusted profile to a resource group, it applies to all clusters in the resource group.

    To assign a trusted profile to a cluster. 

    ```sh
    ibmcloud oc experimental trusted-profile set --trusted-profile PROFILE --cluster CLUSTER [--output OUTPUT] [-q]
    ```
    {: pre}

    `--cluster CLUSTER`
    :   The cluster ID to set the the trusted profile on. To get the cluster ID, run `ibmcloud oc cluster get`. 

    `--trusted-profile PROFILE`
    :   The trusted profile ID. To get the trusted profile ID, run `ibmcloud iam trusted-profiles`.

    `--output OUTPUT`
    :   Prints the command output in the provided format. Accepted values: json

    `-q`
    :   Do not show the message of the day or update reminders.


    To assign a trusted profile to a resource group. 
  
    ```sh
    ibmcloud oc experimental trusted-profile default set --region REGION --resource-group GROUP --trusted-profile PROFILE [--output OUTPUT] [-q]
    ```
    {: pre}

    `--region REGION`
    :   The region where the resource group is located. To get the details of a resource group, run `ibmcloud resource group`.

    `--resource-group GROUP`
    :   The resource group ID to set the trusted profile on. To list your resource groups, run `ibmcloud resource groups`.

    `--trusted-profile PROFILE`
    :   The trusted profile ID. To get the trusted profile ID, run `ibmcloud iam trusted-profiles`.

    `--output OUTPUT`
    :   Prints the command output in the provided format. Accepted values: `json`.

    `-q`
    :   Do not show the message of the day or update reminders.


3. Verify that the trusted profile has been added to the cluster. 

    ```sh
    ibmcloud oc experimental trusted-profile get --cluster CLUSTER
    ```
    {: pre}

    Example output.

    ```sh
    Fetching trusted-profile for the cluster...
    OK
    Cluster a1bc2de45fgh6ijklmn7op is configured with trusted-profile Profile-a12bc34-1111-1111-1234-a123bc456 
    ```
    {: screen}


## Limitations and considerations
{: #tp-limitations}

Review the following limitations and considerations before you use trusted profiles. 

Irreversible transition to trusted profile
:   Once a trusted profile is configured at the cluster or resource group level, reverting to using an API key is not supported. Follow the steps carefully to ensure that the trusted profile is configured correctly. 

Verification scope is limited to the `kube-system` namespace. 
:   Trusted profile trust validation is currently limited to the `kube-system` namespace for Kubernetes and Red Hat OpenShift clusters. Users experimenting with other trusted profile features or configurations outside this scope may encounter issues. 
