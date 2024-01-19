---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-18"


keywords: openshift, openshift data foundation, openshift container storage, trusted profile

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# Setting up trusted profiles for the OpenShift Data Foundation add-on
{: #storage-odf-trusted-profiles}

[Virtual Private Cloud]{: tag-vpc}  [Classic clusters]{: tag-classic-inf}


You can use trusted profiles to limit the access that running pods in your cluster have to other resources in your account or cluster. For more information about trusted profiles, see [Creating trusted profiles](/docs/account?topic=account-create-trusted-profile).
{: shortdesc}



## Enabling the OpenShift Data Foundation add-on
{: #odf-addon-enable-trusted}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. Enable the add-on in your cluster. Review the [Parameter Reference](/docs/openshift?topic=openshift-openshift_storage_parameters).

    Example command:

    ```sh
    ibmcloud oc cluster addon enable openshift-data-foundation -c <cluster-name> --version 4.X.X
    ```
    {: pre}

1. Verify that the add-on state is `normal` and the status is `ready`.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER-ID
    ```
    {: pre}

1. Verify that the metrics agent pod is deployed and the status is `Running`.
    ```sh
    kubectl get pods -n kube-system | grep ibm-storage-metrics-agent
    ```
    {: pre}

    Example output:
    ```sh
    ibm-storage-metrics-agent-644cd95b5b-rh2gd        2/2     Running   0          7h42m
    ```
    {: screen}

## Setting up trusted profiles
{: #odf-setup-trusted}

1. Follow the steps to [create a trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui). In the **Conditions** for the profile, be sure to specify the following access.
    * Allow access when **Namespace** equals `kube-system`
    * Satellite Service Roles - Satellite Link Administrator, Reader
    * Kubernetes Service Roles - Manager, Editor
    * Billing Service Roles - Reader, Operator

1. After you create your trusted profile, copy the ID from the **Trusted profiles** page in the console.

1. Decide if you want to use the **Profile ID** or an **API key** in the Kubernetes secret that the add-on uses. You can create the secret by using the ID or API key for the trusted profile. Save the following text and enter your credentials. You can follow the steps to create the secret manually or you can use the shell script to [automatically create the secret in your cluster](#odf-secret-create-truted-profile).


    Example credentials with pod identity:

    ```txt
    IBMCLOUD_AUTHTYPE=pod-identity
    IBMCLOUD_PROFILEID=<TRUSTED-PROFILE-ID>
    ```
    {: codeblock}
    
    Example credentials with an API key.

    ```txt
    IBMCLOUD_AUTHTYPE=iam
    IBMCLOUD_APIKEY=<API-KEY>
    ```
    {: codeblock}

1. Encode the credentials to base64. 

    ```sh
    echo -n "IBMCLOUD_AUTHTYPE=<IAM-OR-POD-IDENTITY>
    IBMCLOUD_APIKEY=<API-KEY>" | base64
    ```
    {: pre}

1. Create a secret in your cluster that contains the credentials for the trusted profile. Save the following YAML to a file called `ibm-cloud-credentials.yaml`. In the `ibm-credentials.env:` field, enter the base64 encoded API key or the ID of trusted profile.

    ```yaml
    apiVersion: v1
    data:
      ibm-credentials.env: # Trusted profile ID
    kind: Secret
    metadata:
      name: ibm-cloud-credentials
      namespace: kube-system
    type: Opaque
    ```
    {: codeblock}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. Create the secret in your cluster.
    
    ```sh
    kubectl apply -f ibm-cloud-credentials.yaml
    ```
    {: pre}

1. Restart the agent pods.
    ```sh
    kubectl delete pod <ibm-storage-metrics-agent> -n kube-system>
    ```
    {: pre}

### Automatically creating a secret by using a Shell script
{: #odf-secret-create-truted-profile}

1. Follow the steps to [create a trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui). In the **Conditions** for the profile, be sure to specify the following access.
    * Allow access when **Namespace** equals `kube-system`
    * Satellite Service Roles - Satellite Link Administrator, Reader
    * Kubernetes Service Roles - Manager, Editor
    * Billing Service Roles - Reader, Operator


1. Save the following script to a file called `generate-secret.sh`.

    ```sh
    IBMCLOUD_AUTHTYPE= 
    SECRET= 
    
    
    error() { 
        if [[ $? != 0 ]]; then 
            echo "$1"; exit 1 
        fi 
    } 
    
    #validate_arguments validates the arguments provided to the script 
    validate_arguments() { 
        if [[ "$#" -eq 1 ]]; then 
        if [[ "$1" == "-h" ]] || [[ "$1" == "--help" ]]; then 
            usage; exit 1 
        fi 
        fi 

            #number of arguments provided to the script must be 2 
        if [[ "$#" -ne 2 ]]; then 
            echo "Invalid number of arguments provided" 
            usage; exit 1 
        fi 
    
        #1st argument must be 'iam' or 'pod-identity' 
        if [[ "$1" != "iam" ]] && [[ "$1" != "pod-identity" ]]; then 
            echo "Provide a valid auth-type" 
            usage; exit 1 
        fi 
    
        IBMCLOUD_AUTHTYPE=$1 
        SECRET=$2 
    } 
    
    #usage - prints the usage for execution of script 
    usage() { 
        echo "USAGE: 
        bash generate-secret.sh <auth-type> <apikey/profile-id> 
        auth-type: auth-type should be either iam or pod-identity. Provide iam to use api 
    key, pod-identity to use trusted profile" 
    } 
    
    #main 
    main() { 
    
        validate_arguments "$@" 
    
        auth_type="IBMCLOUD_AUTHTYPE=$IBMCLOUD_AUTHTYPE" 
    
        secret= 
    
        if [[ "$IBMCLOUD_AUTHTYPE" == "iam" ]]; then 
            secret="IBMCLOUD_APIKEY=$SECRET" 
        else 
            secret="IBMCLOUD_PROFILEID=$SECRET" 
        fi 
    
        encodedValue=$(echo -e "$auth_type\n$secret" | base64) 
        #on certain os, base64 encoding introduces newline, removing the same here. 
        encodedValue=${encodedValue//$'\n'/} 
    
        #fetch the agent pod name 
        agentPodName=$(kubectl get pods -n kube-system | grep ibm-storage-metrics-agent | awk '{print $1}') 
        error "$(date +"%b %d %G %H:%M:%S"):  Unable to fetch ODF agent pod." 
        if [[ "$agentPodName" == "" ]]; then 
            echo "$(date +"%b %d %G %H:%M:%S"):  Error - ibm-storage-metrics-agent pod 
    not found" 
            exit 1 
        fi 
    
        echo "apiVersion: v1 
    data: 
    ibm-credentials.env: $encodedValue 
    kind: Secret 
    metadata: 
    name: ibm-cloud-credentials 
    namespace: kube-system 
    type: Opaque" > ibm-cloud-credentials.yaml 
    
        #create the k8s secret 
        kubectl apply -f ibm-cloud-credentials.yaml &> /dev/null 
        error "$(date +"%b %d %G %H:%M:%S"):  Error creating ibm-cloud-credentials 
    secret." 
        echo "$(date +"%b %d %G %H:%M:%S"):  Created ibm-cloud-credentials secret" 
    
        #restart the ODF agent pod 
        echo "$(date +"%b %d %G %H:%M:%S"):  Restarting $agentPodName pod" 
        kubectl delete pod "$agentPodName" -n kube-system &> /dev/null 
        error "$(date +"%b %d %G %H:%M:%S"):  Error restarting $agentPodName pod in 
    kube-system namespace." 
    
        agentPodStatus= 
        for i in {1..12} 
        do 
            sleep 5 
            agentPodStatus=$(kubectl get pods -n kube-system | grep ibm-storage-metrics-agent | awk '{print $3}') 
            if [[ "$agentPodStatus" == "Running" ]]; then 
                echo "$(date +"%b %d %G %H:%M:%S"):  $i: ODF billing agent is now using 
    ibm-cloud-credentials secret" 
                rm ibm-cloud-credentials.yaml 
                error "Error deleting ibm-cloud-credentials.yaml." 
                exit 0 
            fi 
        done 
    
        error "$(date +"%b %d %G %H:%M:%S"):  Error - ibm-storage-metrics-agent is in 
    $agentPodStatus state" 
    } 
    
    main "$@" 
    ```
    {: codeblock}

1. Run the `generate-secret.sh` script and specify `iam` or `pod-identity` as the `IBMCLOUD_AUTHTYPE` and your `PROFILE-ID` or `API-KEY`.

    Example command to run `generate-secret.sh` by using `pod-identity` with your trusted profiled ID.
    ```sh
    sh ./generate-secret.sh pod-identity PROFILE-ID
    ```
    {: pre}


    Example command to run `generate-secret.sh` by using `iam` with an API key.
    ```sh
    sh ./generate-secret.sh iam API-KEY
    ```
    {: pre}

1. Restart the agent pods.
    ```sh
    oc delete pod <ibm-storage-metrics-agent> -n kube-sysem
    ```
    {: pre}

1. Get the logs of the agent pod to verify the driver is using the correct credentials by looking for the `secret type` in the output. For example,`"secret-used":"ibm-cloud-credentials","type":"pod-identity"`.

    ```sh
    oc logs ibm-storage-metrics-agent-xxx -c storage-secret-sidecar -n kube-system
    ```
    {: pre}





