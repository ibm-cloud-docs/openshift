---

copyright: 
  years: 2014, 2023
lastupdated: "2023-08-23"

keywords: openshift, clusters, worker nodes, worker pools, add, sgx

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Installing SGX drivers and platform software on SGX-capable worker nodes
{: #sgx-install}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic}

Intel Software Guard Extensions (SGX) is a technology that can protect data-in-use through hardware-based server security. With Intel SGX, you can protect select code and data from disclosure or modification. Through the use of trusted execution environments (TEE), known as enclaves, you can encrypt the pieces of your app memory that contain sensitive data while the data or code is being used. To use Intel SGX, you must install the SGX drivers and platform software on SGX-capable worker nodes. Then, design your app to run in an SGX environment.
{: shortdesc}

![An example SGX application.](images/cc-iks.png){: caption="Figure. Example SGX application set up" caption-side="bottom"}

When you develop a confidential computing application, you must design it in a way that you can segment the information that needs to be encrypted. At runtime, the segmented information is kept confidential through attestation. When a request for information from the segmented code or app data is received, the enclave verifies that the request comes from the part of the application that exists outside of the enclave within the same application before sharing any information. Through the attestation process, information is kept confidential and data leakage is prevented.



## Installing with a script
{: #intel-sgx-script}

Before you begin, create a worker pool with SGX-capable worker nodes. To work with Intel SGX, you must use one of the following machine types: `me4c.4x32` and `me4c.4x32.1.9tb.ssd`.


1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Create an `sgx-admin` project with a privileged security context constraint that is added to the project service account so that the drivers and platform software can pull and run the required images.

    ```sh
    curl -fssl https://raw.githubusercontent.com/ibm-cloud-security/data-shield-reference-apps/master/scripts/sgx-driver-psw/config_openshift/create_openshift_config.sh | bash
    ```
    {: codeblock}

1. Create a daemon set to install the drivers and platform software on your SGX-capable worker nodes.

    ```sh
    oc create -f https://raw.githubusercontent.com/ibm-cloud-security/data-shield-reference-apps/master/scripts/sgx-driver-psw/install_sgx/deployment_install_sgx_openshift.yaml
    ```
    {: codeblock}

1. Verify that the drivers and platform software were installed by running the following command to check for a pod that begins with `sgx-installer`.

    ```sh
    oc get pods
    ```
    {: codeblock}

1. Get the logs for your `sgx-installer` pod to verify that you see the messages `SGX driver installed` and `PSW installed`.

    ```sh
    oc logs <name_of_SGX_installer_pod>
    ```

1. Now that the drivers and platform software are installed, remove the daemon set.

    ```sh
    oc delete daemonset sgx-installer
    ```
    {: codeblock}

1. Delete the security context and service account that you created.

    ```sh
    oc delete scc sgx-admin
    oc delete serviceaccount sgx-admin
    ```
    {: codeblock}

Now, you can develop your confidential computing app to use the enclave for sensitive data.

To uninstall the drivers and platform software, you can follow the same steps, but with the following installation command: `oc create -f https://raw.githubusercontent.com/ibm-cloud-security/data-shield-reference-apps/master/scripts/sgx-driver-psw/uninstall_sgx/deployment_uninstall_sgx_openshift.yaml`
{: note}


