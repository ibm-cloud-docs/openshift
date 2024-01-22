---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-22"


keywords: secret, certificate, field, tls, non-tls, rotate, ingress

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Managing TLS and non-TLS certificates and secrets
{: #secrets}

Learn how you can use certificates and secrets in your cluster. 
{: shortdesc}

Consider using [{{site.data.keyword.secrets-manager_short}}](/docs/openshift?topic=openshift-secrets-mgr) to centrally manage and automatically update your secrets. 
{: tip}

## Managing TLS certificates and secrets with Ingress
{: #tls}

Your Ingress TLS certificate is stored as a Kubernetes secret. To manage the TLS secrets in your cluster, you can use the `ibmcloud oc ingress secret` set of commands. 
{: shortdesc}

For example, you can import a certificate from {{site.data.keyword.secrets-manager_short}} to a Kubernetes secret in your cluster by running the following command.

```sh
ibmcloud oc ingress secret create --cluster <cluster_name_or_ID> --cert-crn <crn> --name <secret_name> --namespace openshift-ingress
```
{: pre}

To import the certificate with the `ibmcloud oc ingress secret create` command, you must have a default [{{site.data.keyword.secrets-manager_short}}](/docs/openshift?topic=openshift-secrets-mgr) instance registered to your cluster. If you do not have a {{site.data.keyword.secrets-manager_short}} instance and your secrets are instead written directly to your cluster, your secrets do not have the required CRN value and you must manually copy them with the OpenShift `oc` plug-in [commands](https://docs.openshift.com/container-platform/4.14/cli_reference/openshift_cli/developer-cli-commands.html){: external}. 
{: important}

To view all Ingress secrets for TLS certificates in your cluster, run the following command.

```sh
ibmcloud oc ingress secret ls -c <cluster>
```
{: pre}

### Setting up TLS secrets for the IBM-provided Ingress subdomain
{: #tls-default}

IBM provides an Ingress subdomain and a default TLS certificate, stored as a Kubernetes secret in your cluster, that you can specify in your Ingress resource. IBM-provided TLS certificates are signed by LetsEncrypt and are fully managed by IBM. 
{: shortdesc}

The IBM-provided Ingress subdomain wildcard, `*.<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`, is registered by default for your cluster. The IBM-provided TLS certificate is a wildcard certificate and can be used for the wildcard subdomain.
{: tip}

Follow the steps to use the default TLS certificate for the IBM-provided Ingress subdomain.

1. Get the name of the secret where your default TLS certificate is stored. Note that this is the secret name you specify in the `spec.tls` section of your Ingress resource.

    ```sh
    ibmcloud oc cluster get -c <cluster> | grep Ingress
    ```
    {: pre}

    Example output

    ```sh
    Ingress Subdomain:      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
    Ingress Secret:         mycluster-<hash>-0000
    ```
    {: screen}

2. View the secret details and note the CRN value. This is the CRN of the TLS certificate. If you do not have a default [{{site.data.keyword.secrets-manager_short}}] instance registered to your cluster, your secret does not have a CRN. See the note in the following step for more details. 


    ```sh
    ibmcloud oc ingress secret get -c <cluster> --name <secret_name> --namespace openshift-ingress
    ```
    {: pre}

3. Create a secret for the default TLS certificate in each namespace where your Ingress resources or apps exist. Specify the TLS certificate CRN with the `--cert-crn` command option. 

    ```sh
    ibmcloud oc ingress secret create --cluster <cluster_name_or_ID> --cert-crn <CRN> --name <secret_name> --namespace openshift-ingress
    ```
    {: pre}

    To copy the secret with the **`ibmcloud oc ingress secret create`** command, you must have a default [{{site.data.keyword.secrets-manager_short}}](/docs/openshift?topic=openshift-secrets-mgr) instance registered to your cluster. If you do not have a {{site.data.keyword.secrets-manager_short}} instance and your secrets are instead written directly to your cluster, your secrets do not have the required CRN value and you must manually copy them with the OpenShift `oc` plug-in [commands](https://docs.openshift.com/container-platform/4.14/cli_reference/openshift_cli/developer-cli-commands.html){: external}. 
    {: important}



### Setting up TLS secrets for custom subdomains
{: #tls-custom}

If you define a custom subdomain in your Ingress resource, you can use your own TLS certificate to manage TLS termination. You must create a Kubernetes secret to store the TLS certificate, then import this secret into each namespace where your apps exist.
{: shortdesc}

By storing custom TLS certificates in [{{site.data.keyword.secrets-manager_short}}](/docs/openshift?topic=openshift-secrets-mgr), you can import your certificates directly into a Kubernetes secret in your cluster. 
{: tip}

1. Create or import a secret for the TLS certificate in the namespace where your Ingress resource exists. For example, you can import a secret from {{site.data.keyword.secrets-manager_short}} into your cluster by running the following command. Specify the TLS certificate's CRN with the `--cert-crn` command option.

  To import the certificate with the `ibmcloud oc ingress secret create` command, you must have a default [{{site.data.keyword.secrets-manager_short}}](/docs/openshift?topic=openshift-secrets-mgr) instance registered to your cluster. If you do not have a {{site.data.keyword.secrets-manager_short}} instance and your secrets are instead written directly to your cluster, your secrets do not have the required CRN value and you must manually copy them with the OpenShift `oc` plug-in [commands](https://docs.openshift.com/container-platform/4.14/cli_reference/openshift_cli/developer-cli-commands.html){: external}. 
  {: important}


    ```sh
    ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> --namespace openshift-ingress
    ```
    {: pre}

2. Repeat the previous step for each namespace where your apps exist. 


## Managing non-TLS secrets
{: #non-tls}

To manage non-TLS secrets, you can use the `ibmcloud oc ingress secret` commands. 
{: shortdesc}

There are 4 types of non-TLS secrets:
- **Arbitrary secrets** hold one string value. 
- **IAM credentials** hold an IAM API key.
- **Username and password secrets** hold a username and password as two separate values.
- **Key values** hold JSON values. 

Learn how you can centrally manage your non-TLS secrets with [{{site.data.keyword.secrets-manager_full_notm}}](/docs/openshift?topic=openshift-secrets-mgr). With {{site.data.keyword.secrets-manager_short}}, you can create managed Kubernetes secrets, update your secrets automatically, create secret groups that control who has access to the secrets in your cluster, and more.
{: tip} 


### Creating a non-TLS secret in your cluster
{: #non-tls-create}

Create a non-TLS secret by specifying the `--type Opaque` option in the **`ibmcloud oc ingress secret create`** command. With the `Opaque` type, you can include multiple non-certificate CRN values. If the `--type` option is not specified, TLS is applied by default. For more information and additional command options, see the [CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_create).
{: shortdesc}

The following example command creates a non-TLS secret with the `Opaque` type specified. Non-TLS secrets require at least one secret [field](#non-tls-field-add). Note that how you specify the `--field` option varies [based on the type of secret you create](#non-tls-field-add). 

```sh
ibmcloud oc ingress secret create -c cluster-test --name example-secret --namespace openshift-ingress --field crn:v1:bluemix:public:secrets-manager:us-south:a/1aa111aa1a11111aaa1a1111aa1aa111:111a1111-11a1 --type Opaque 
```
{: pre}

To verify that the secret is created, list all secrets in the namespace.

```sh
kubectl get secret -n default
```
{: pre}

The following example shows the output.
```sh
NAME                   TYPE                                  DATA   AGE
all-icr-io             kubernetes.io/dockerconfigjson        1      41h
default-token-8t6xw    kubernetes.io/service-account-token   3      41h
example-secret         Opaque                                        3m
```
{: screen}

### Managing non-TLS secret fields
{: #non-tls-field}

A secret field is a key-value pair that is stored in a non-TLS secret. Refer to the following examples to view, add, update, or remove non-TLS secret fields.
{: shortdesc}

#### Viewing field values
{: #non-tls-field-view}

You can view the values of a secret's fields by getting the details of the secret.
{: shortdesc}

```sh
kubectl get secret -n default example-secret -o yaml
```
{: pre} 

The following example output shows the secret fields and their values in the `data` section.

```yaml
apiVersion: v1
data:
  arbitraryFVT: AAAaaAAaAAA1AAAaaAAa
  userCredsFVT_password: aAAaa1aaaA=
  userCredsFVT_username: aAAaaa==
kind: Secret
metadata:
  annotations:
    ingress.cloud.ibm.com/cert-source: ibm
    razee.io/build-url: https://travis.ibm.com/alchemy-containers/armada-ingress-secret-mgr/builds/78876583
    razee.io/source-url: https://github.ibm.com/alchemy-containers/armada-ingress-secret-mgr/commit/651fa822632128163cf638c47f0a14b1e0e2915a
  creationTimestamp: "2022-11-08T19:45:05Z"
  name: example-secret
  namespace: default
  resourceVersion: "111111"
  uid: 1aaa1111-1a11-111a-a1a1-11111a1a1a1a
type: Opaque
```
{: screen}

You can also list the fields in a secret with the `ibmcloud oc ingress secret field ls` and `ibmcloud oc ingress secret get` commands, but the outputs include only the field name and not the value associated with it. 

#### Adding a secret field
{: #non-tls-field-add}

Add a secret field to a non-TLS secret by running the [`ibmcloud oc ingress secret field add`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_field_add) command with the `--field` option. You can also use this option to add fields when you create a secret with the [**`ibmcloud oc ingress secret create`**](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_create) command. This option is not supported for TLS secrets. 
{: shortdesc}

There are three ways to specify the `--field` option. The one you choose depends on the secret type and how you want to name the field in the secret.

| Option | Format | Description | Supported secret types |
| ------ | ------ | ----------- | ---------------------- |
| Default | `--field <crn>` | The name of the added field is the [default field name](#default-field-name) for the secret type of the given CRN. | All non-TLS secret types |
| Named | `--field <name>=<crn>` | Use this option to specify a name for the added field. The name of the added field is the value specified for `<name>`. | - Arbitrary \n - IAM credentials |
| Prefixed | `--field prefix=<crn>` | The name of the added field is the [default field name](#default-field-name) for the secret type specified by the given CRN, prefixed by the name of the secret specified by the `<crn>` and an underscore. | - IAM credentials \n - username/password \n - key/value |
{: caption="Options for adding fields to non-TLS secrets"}


The default field names are `arbitrary` for arbitrary secrets, `api_key` for IAM credentials, `username` or `password` for user credentials, and `key` for key-value.{: #default-field-name}

The following example adds three secret fields - using the same IAM credentials secret, named `iam` - to demonstrate how the different `--field` options affect the resulting field name. You can [view the fields](#non-tls-field-view) added to a secret by running `kubectl get secret` and viewing the `data` block of the output. 

```sh
ibmcloud oc ingress secret field add --cluster example-cluster --name example-iam-secret --namespace openshift-ingress  --field crn:v1:bluemix:public:secrets-manager:us-south:a/1aa111aa-1a11-111a-aa1a-1111aa1aa111:secret:111a1111-11a1-11aa-a1a1-111aa12345aa --field custom_iam_name=crn:v1:bluemix:public:secrets-manager:us-south:a/1aa111aa-1a11-111a-aa1a-1111aa1aa111:secret:111a1111-11a1-11aa-a1a1-111aa12345aa --field prefix=crn:v1:bluemix:public:secrets-manager:us-south:a/1aa111aa-1a11-111a-aa1a-1111aa1aa111:secret:111a1111-11a1-11aa-a1a1-111aa12345aa
```
{: pre}

Example fields listed in the `data` block of the secret details. 

```sh
data:
  api_key: bmZrUHR1VS1fNVpMOExsTmIxeTdQcXFTSENMc2pTUjRsNTQyTzZkZ2ZQMkk=  # Default field type using the default `api_key` field name
  custom_iam_name: bmZrUHR1VS1fNVpMOExsTmIxeTdQcXFTSENMc2pTUjRsNTQyTzZkZ2ZQMkk=  # Named field type using the specified `custom_iam_name` field name.
  iam_api_key: bmZrUHR1VS1fNVpMOExsTmIxeTdQcXFTSENMc2pTUjRsNTQyTzZkZ2ZQMkk= # Prefixed field type using the `iam` name in Secrets Manager followed by the `api_key` default name.
```
{: screen}


#### Updating secret fields
{: #non-tls-field-update}

Run the **`ingress secret update`** command to update a secret field's values. Note that this does not update the CRN. For more information and command options, see the [CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_update).
{: #shortdesc}

```sh
ibmcloud oc ingress secret update --cluster example-cluster --name example-secret --namespace openshift-ingress
```
{: pre}

#### Removing a secret field
{: #non-tls-field-rm}

You can remove a secret field from a non-TLS secret. For more information and command options, see the [CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_ingress_secret_field_add).
{: shortdesc}

```sh
ibmcloud oc ingress secret field rm -c example-cluster --name example-secret --namespace openshift-ingress --field-name example-Field
```
{: pre}

You can verify that the field is removed by checking the `data` block of the secret's details. 

```sh
kubectl get secret -n default example-secret -o yaml
```
{: pre} 

## Secrets FAQ
{: #secrets-faq}

Review the answers to commonly asked questions about managing secrets in your cluster.
{: shortdesc}

Are my secrets automatically updated if I do not create and register a [{{site.data.keyword.secrets-manager_short}}](/docs/openshift?topic=openshift-secrets-mgr) instance?
:    If you do not register a {{site.data.keyword.secrets-manager_short}} instance to your cluster, your default Ingress secrets continue to update automatically every 90 days and are applied to your cluster. However, any secrets you created that *reference* the default Ingress secret are not automatically updated. 
:   **Example scenario**: You have a default Ingress certificate in the `default` namespace. You run the **`ibmcloud oc ingress secret create`** command and reference the CRN of the default Ingress certificate to mirror the certificate in the `istio-system` namespace. Without a {{site.data.keyword.secrets-manager_short}} instance, the default Ingress certificate in the `default` namespace automatically updates. However, you are responsible for regularly updating the certificate in the `istio-system` namespace with the `**kubectl**` commands or another rotation method. 

I created secrets that reference the default Ingress certificate, but I did not create and register a [{{site.data.keyword.secrets-manager_short}}](/docs/openshift?topic=openshift-secrets-mgr) instance. How do I manage my secrets?
:   If you don't register a {{site.data.keyword.secrets-manager_short}} instance, {{site.data.keyword.openshiftlong_notm}} automatically updates only the default Ingress secret. You are responsible for managing any other secrets by using **`kubectl`** commands or another rotation method. If your secrets reference the default Ingress certificate, remove them by using **`ibmcloud ks ingress secret rm`**.



