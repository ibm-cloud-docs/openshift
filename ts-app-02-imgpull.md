---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-19"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why do images fail to pull from registry with `ImagePullBackOff` or authorization errors?
{: #ts-app-image-pull}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


When you deploy a workload that pulls an image from {{site.data.keyword.registrylong_notm}}, your pods fail with an **`ImagePullBackOff`** status.
{: tsSymptoms}

```sh
oc get pods
```
{: pre}

```sh
NAME         READY     STATUS             RESTARTS   AGE
<pod_name>   0/1       ImagePullBackOff   0          2m
```
{: screen}

When you describe the pod, you see authentication errors similar to the following.

```sh
oc describe pod <pod_name>
```
{: pre}

```sh
Failed to pull image "<region>.icr.io/<namespace>/<image>:<tag>" ... unauthorized: authentication required
Failed to pull image "<region>.icr.io/<namespace>/<image>:<tag>" ... 401 Unauthorized
```
{: screen}

```sh
Failed to pull image "registry.ng.bluemix.net/<namespace>/<image>:<tag>" ... unauthorized: authentication required
Failed to pull image "registry.ng.bluemix.net/<namespace>/<image>:<tag>" ... 401 Unauthorized
```
{: screen}


Your cluster uses an API key that is stored in an [image pull secret](/docs/openshift?topic=openshift-registry#cluster_registry_auth) to authorize the cluster to pull images from {{site.data.keyword.registrylong_notm}}.
{: tsCauses}

By default, new clusters have image pull secrets that use API keys so that the cluster can pull images from any regional `icr.io` registry for containers that are deployed to the `default` {{site.data.keyword.openshiftshort}} project.


1. Verify that you use the correct name and tag of the image in your deployment YAML file.
{: tsResolve}

    ```sh
    ibmcloud cr images
    ```
    {: pre}

2. Check your [pull traffic and storage quota](/docs/Registry?topic=Registry-registry_quota). If the limit is reached, free up used storage or ask your registry administrator to increase the quota.
    ```sh
    ibmcloud cr quota
    ```
    {: pre}

3. Get the pod configuration file of a failing pod, and look for the `imagePullSecrets` section.
    ```sh
    oc get pod <pod_name> -o yaml
    ```
    {: pre}

    Example output

    ```sh
    ...
    imagePullSecrets:
    - name: all-icr-io
    ...
    ```
    {: screen}

4. If no image pull secrets are listed, set up the image pull secret in your project.
    1. Verify that the `default` project has `icr-io` image pull secrets for each regional registry that you want to use. If no `icr-io` secrets are listed in the project, [use the `ibmcloud oc cluster pull-secret apply --cluster <cluster_name_or_ID>` command](/docs/openshift?topic=openshift-registry#imagePullSecret_migrate_api_key) to create the image pull secrets in the `default` project.
        ```sh
        oc get secrets -n default | grep "icr-io"
        ```
        {: pre}

    2. [Copy the `all-icr-io` image pull secret from the `default` {{site.data.keyword.openshiftshort}} project to the project where you want to deploy your workload](/docs/openshift?topic=openshift-registry#copy_imagePullSecret).
    3. [Add the image pull secret to the service account for this {{site.data.keyword.openshiftshort}} project](/docs/openshift?topic=openshift-registry#store_imagePullSecret) so that all pods in the project can use the image pull secret credentials.
5. If image pull secrets are listed in the pod, determine what type of credentials you use to access {{site.data.keyword.registrylong_notm}}.
    * If the secret has `icr` in the name, you use an API key to authenticate with the `icr.io` domain names. Continue with [Troubleshooting image pull secrets that use API keys](#img-pull-api-key).
    * If you have both types of secrets, then you use both authentication methods. Going forward, use the `icr.io` domain names in your deployment YAMLs for the container image. Continue with [Troubleshooting image pull secrets that use API keys](#img-pull-api-key).



## Troubleshooting image pull secrets that use API keys
{: #img-pull-api-key}

If your pod configuration has an image pull secret that uses an API key, check that the API key credentials are set up correctly.
{: shortdesc}

The following steps assume that the API key stores the credentials of a service ID. If you set up your image pull secret to use an API key of an individual user, you must verify that user's {{site.data.keyword.cloud_notm}} IAM permissions and credentials.
{: note}

1. Find the service ID that API key uses for the image pull secret by reviewing the **Description**. The service ID that is created with the cluster is named `cluster-<cluster_ID>` and is used in the `default` {{site.data.keyword.openshiftshort}} project. If you created another service ID such as to access a different {{site.data.keyword.openshiftshort}} project or to modify {{site.data.keyword.cloud_notm}} IAM permissions, you customized the description.
    ```sh
    ibmcloud iam service-ids
    ```
    {: pre}

    Example output

    ```sh
    UUID                Name               Created At              Last Updated            Description                                                                                                                                                                                         Locked
    ServiceId-aa11...   <service_ID_name>  2019-02-01T19:01+0000   2019-02-01T19:01+0000   ID for <cluster_name>                                                                                                                                         false
    ServiceId-bb22...   <service_ID_name>  2019-02-01T19:01+0000   2019-02-01T19:01+0000   Service ID for IBM Cloud Container Registry in Kubernetes cluster <cluster_name> namespace <project>                                                                                                                                         false
    ```
    {: screen}

2. Verify that the service ID is assigned at least an {{site.data.keyword.cloud_notm}} IAM **Reader** [service access role policy for {{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-user#create). If the service ID does not have the **Reader** service access role, [edit the IAM policies](/docs/account?topic=account-serviceids#update_serviceid). If the policies are correct, continue with the next step to see if the credentials are valid.
    ```sh
    ibmcloud iam service-policies <service_ID_name>
    ```
    {: pre}

    Example output

    ```sh
    Policy ID:   a111a111-b22b-333c-d4dd-e555555555e5
    Roles:       Reader
    Resources:
                  Service Name       container-registry
                  Service Instance
                  Region
                  Resource Type      namespace
                  Resource           <registry_namespace>
    ```
    {: screen}

3. Check if the image pull secret credentials are valid.
    1. Get the image pull secret configuration. If the pod is not in the `default` project, include the `-n` flag.
        ```sh
        oc get secret <image_pull_secret_name> -o yaml [-n <project>]
        ```
        {: pre}

    2. In the output, copy the base64 encoded value of the `.dockerconfigjson` field.
        ```yaml
        apiVersion: v1
        kind: Secret
        data:
          .dockerconfigjson: eyJyZWdp...==
        ...
        ```
        {: screen}

    3. Decode the base64 string. For example, on OS X you can run the following command.
        ```sh
        echo -n "<base64_string>" | base64 --decode
        ```
        {: pre}

        Example output
        ```sh
        {"auths":{"<region>.icr.io":{"username":"iamapikey","password":"<password_string>","email":"<name@abc.com>","auth":"<auth_string>"}}}
        ```
        {: screen}

    4. Compare the image pull secret regional registry domain name with the domain name that you specified in the container image. By default, new clusters have image pull secrets for each regional registry domain name for containers that run in the `default` {{site.data.keyword.openshiftshort}} project. However, if you modified the default settings or are using a different {{site.data.keyword.openshiftshort}} project, you might not have an image pull secret for the regional registry. [Copy an image pull secret](/docs/openshift?topic=openshift-registry#copy_imagePullSecret) for the regional registry domain name.
    5. Log in to the registry from your local machine by using the `username` and `password` from your image pull secret. If you cannot log in, you might need to fix the service ID.
        ```sh
        docker login -u iamapikey -p <password_string> <region>.icr.io
        ```
        {: pre}

        1. Re-create the cluster service ID, {{site.data.keyword.cloud_notm}} IAM policies, API key, and image pull secrets for containers that run in the `default` {{site.data.keyword.openshiftshort}} project.
            ```sh
            ibmcloud oc cluster pull-secret apply --cluster <cluster_name_or_ID>
            ```
            {: pre}

        2. Re-create your deployment in the `default` {{site.data.keyword.openshiftshort}} project. If you still see an authorization error message, repeat Steps 1-5 with the new image pull secrets. If you still cannot log in, [open an {{site.data.keyword.cloud_notm}} Support case](/docs/containers?topic=containers-get-help).

    6. If the login succeeds, pull an image locally. If the command fails with an `access denied` error, the registry account is in a different {{site.data.keyword.cloud_notm}} account than the one your cluster is in. [Create an image pull secret to access images in the other account](/docs/openshift?topic=openshift-registry#other_registry_accounts). If you can pull an image to your local machine, then your API key has the right permissions, but the API setup in your cluster is not correct. 
        ```sh
        docker pull <region>icr.io/<namespace>/<image>:<tag>
        ```
        {: pre}

    7. Check that the pull secret is either referenced directly from the deployment or from the service account that the deployment uses. If you still can't resolve the issue, [contact support](/docs/containers?topic=containers-get-help).









