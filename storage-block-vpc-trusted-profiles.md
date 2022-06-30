---

copyright: 
  years: 2014, 2022
lastupdated: "2022-06-30"

keywords: openshift, block storage, pod identity, trusted profiles

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Setting up trusted profiles for the {{site.data.keyword.block_storage_is_short}} add-on
{: #storage-block-vpc-trusted-profiles}

You can use trusted profiles to limit the access that running pods in your cluster have to other resources in your account or cluster. For more information about trusted profiles, see [Creating trusted profiles](/docs/account?topic=account-create-trusted-profile).
{: shortdesc}

Supported infrastructure provider
:   ![VPC](../icons/vpc.svg "VPC") VPC

## Enabling the {{site.data.keyword.block_storage_is_short}} add-on
{: #vpc-addon-enable-trusted}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Get the version number of the `vpc-block-csi-driver` add-on that is installed in your cluster.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER
    ```
    {: pre}


1. If you have an add-on version earlier than 4.4 of the {{site.data.keyword.block_storage_is_short}} add-on installed in your cluster, you must first disable the add-on and then enable version 4.4 or later. 
    ```sh
    ibmcloud oc cluster addon disable vpc-block-csi-driver  --cluster CLUSTER-ID
    ```
    {: pre}

    ```sh
    ibmcloud oc cluster addon enable vpc-block-csi-driver --version 4.4 --cluster CLUSTER-ID
    ```
    {: pre}

    Example output.
    ```sh
    Enabling add-on vpc-block-csi-driver(4.4) for cluster CLUSTER-ID
    The add-on might take several minutes to deploy and become ready for use.
    ```
    {: screen}

1. Verify that the add-on state is `normal` and the status is `ready`.
    ```sh
    ibmcloud oc cluster addon ls --cluster CLUSTER-ID
    ```
    {: pre}

    ```sh
    Name                   Version                     Health State   Health Status   
    vpc-block-csi-driver   4.4 (4.3 default)   normal         Addon Ready. For more info: http://ibm.biz/addon-state (H1500)   
    ```
    {: screen}

    
1. Verify that the driver pods are deployed and the status is `Running`.
    ```sh
    kubectl get pods -n kube-system | grep block
    ```
    {: pre}
    
    Example output
    ```sh                    
    ibm-vpc-block-csi-controller-0                        7/7     Running   0          77s
    ibm-vpc-block-csi-node-56c85                          4/4     Running   0          77s
    ibm-vpc-block-csi-node-87j2t                          4/4     Running   0          77s
    ibm-vpc-block-csi-node-cmh2h                          4/4     Running   0          77s
    ```
    {: screen}


## Setting up trusted profiles
{: #vpc-block-setup-trusted}

1. Follow the steps to [create a trusted profile](/docs/account?topic=account-create-trusted-profile&interface=ui). In the **Conditions** for the profile, be sure to specify the following access.

    * Allow access when **Service account** equals `ibm-vpc-block-controller-sa`.
    * Allow acccess when **Namespace** equals `kube-system`.

    You can create the trusted profile for specific clusters or for all current and future clusters.
    {: note}
    
1. After you create your trusted profile, copy the ID from the **Trusted profiles** page in the console.

1. Decide if you want to use the **Profile ID** or an **API key** in the Kubernetes secret that the add-on uses. Save the following text and enter your credentials. You can follow the steps to create the secret manually or you can use the shell script to [automatically create the secret in your cluster](#secret-create-truted-profile).

    Example credentials with pod identity
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

1. Create a secret in your cluster that contains the credentials for the trusted profile. You can create the secret by using the ID or API key for the trusted profile. Save the following YAML to a file called `ibm-cloud-credentials.yaml`. In the `ibm-credentials.env:` field, enter the base64 encoded API key or the ID of trusted profile.

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

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

1. Create the secret in your cluster.
    
    ```sh
    kubectl apply -f ibm-cloud-credentials.yaml
    ```
    {: pre}

1. Restart the driver pods by disabling and re-enabling the add-on.
    1. Disable the add-on. 
        ```sh
        ibmcloud oc cluster addon disable vpc-block-csi-driver
        ```
        {: pre}

    1. Re-enable the add-on.
        ```sh
        ibmcloud oc cluster addon enable vpc-block-csi-driver --cluster CLUSTER --version VERSION
        ```
        {: pre}
    
### Automatically creating a secret by using a Shell script
{: #secret-create-truted-profile}

1. Save the following script to a file called `generate-secret.sh`.

    ```sh
    #!/bin/bash

    IBMCLOUD_AUTHTYPE=
    SECRET=


    error() {
        if [[ $? != 0 ]]; then
            echo $1; exit 1
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
    	auth-type: auth-type should be either iam or pod-identity. Provide iam to use api key, pod-identity to use trusted profile"
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

        #fetch the controller pod name
        controllerPodName=$(kubectl get pods -n kube-system | grep ibm-vpc-block-csi-controller | awk '{print $1}')
        error "$(date +"%b %d %G %H:%M:%S"):  Unable to fetch controller pod."
        if [[ "$controllerPodName" == "" ]]; then
            echo "$(date +"%b %d %G %H:%M:%S"):  VPC Block CSI Driver addon is not enabled"
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
        error "$(date +"%b %d %G %H:%M:%S"):  Error creating ibm-cloud-credentials secret."
        echo "$(date +"%b %d %G %H:%M:%S"):  Created ibm-cloud-credentials secret"

        #restart the controller pod
        echo "$(date +"%b %d %G %H:%M:%S"):  Restarting $controllerPodName pod"
        kubectl delete pod $controllerPodName -n kube-system &> /dev/null
        error "$(date +"%b %d %G %H:%M:%S"):  Error restarting $controllerPodName pod in kube-system namespace."

        controllerPodStatus=
        for i in {1..12}
        do
            sleep 5
            controllerPodStatus=$(kubectl get pods -n kube-system | grep ibm-vpc-block-csi-controller | awk '{print $3}')
            if [[ "$controllerPodStatus" == "Running" ]]; then
                echo "$(date +"%b %d %G %H:%M:%S"):  VPC Block CSI Driver is now using ibm-cloud-credentials secret"
                rm ibm-cloud-credentials.yaml
                error "Error deleting ibm-cloud-credentials.yaml."
                exit 0
            fi
        done

        error "$(date +"%b %d %G %H:%M:%S"):  Error - ibm-vpc-block-csi-controller is in $controllerPodStatus state"
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

1. After the secret is created in your your cluster, disable and re-enable the add-on.

    ```sh
    ibmcloud oc cluster addon disable vpc-block-csi-driver  --cluster CLUSTER-ID
    ```
    {: pre}

    ```sh
    ibmcloud oc cluster addon enable vpc-block-csi-driver --version 4.4 --cluster CLUSTER-ID
    ```
    {: pre}
    
1. Get the logs of the driver pod to verify the driver is using the correct credentials by looking for the `secret type` in the output. For example,`"secret-used":"ibm-cloud-credentials","type":"pod-identity"}`.

    ```sh
    kubectl logs ibm-vpc-block-csi-controller-0 -c storage-secret-sidecar -n kube-system
    ```
    {: pre}
