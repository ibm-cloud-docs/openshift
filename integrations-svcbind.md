---

copyright: 
  years: 2014, 2022
lastupdated: "2022-01-20"

keywords: kubernetes, openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Adding services by using IBM Cloud service binding
{: #service-binding}

Add {{site.data.keyword.cloud_notm}} services to enhance your {{site.data.keyword.openshiftshort}} cluster with extra capabilities in areas such as {{site.data.keyword.watson}} AI, data, security, and Internet of Things (IoT).
{: shortdesc}

## About service binding
{: #svc-bind-about}

Review the following frequently asked questions about service binding.
{: shortdesc}

### What types of services can I bind to my cluster?
{: #svc-bind-types}

When you add {{site.data.keyword.cloud_notm}} services to your cluster, you can choose between services that are enabled for {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) and services that are based on Cloud Foundry. IAM-enabled services offer more granular access control and can be managed in an {{site.data.keyword.cloud_notm}} resource group. Cloud Foundry services must be added to a Cloud Foundry organization and space, and can't be added to a resource group. To control access to your Cloud Foundry service instance, you use Cloud Foundry roles. For more information about IAM-enabled services and Cloud Foundry services, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).

To find a list of supported {{site.data.keyword.cloud_notm}} services, see the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog).

### What is {{site.data.keyword.cloud_notm}} service binding?
{: #svc-bind-what}

Service binding is a quick way to create service credentials for an {{site.data.keyword.cloud_notm}} service by using its public cloud service endpoint and storing these credentials in a Kubernetes secret in your cluster. To bind a service to your cluster, you must provision an instance of the service first. Then, you use the `ibmcloud oc cluster service bind` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_service_bind) to create the service credentials and the Kubernetes secret. The Kubernetes secret is automatically encrypted in etcd to protect your data.

Want to make your secrets even more secured? Ask your cluster admin to [enable a key management service provider](/docs/openshift?topic=openshift-encryption#keyprotect) in your cluster to encrypt new and existing secrets, such as the secret that stores the credentials of your {{site.data.keyword.cloud_notm}} service instances.
{: tip}

### I already have an {{site.data.keyword.cloud_notm}} service. Can I still use {{site.data.keyword.cloud_notm}} service binding?
{: #svc-bind-existing}

Yes, you can use services that meet naming requirements and reuse the service credentials.

* **Naming**: Make sure that the service name is in the following regex format. Example permitted names are `myservice` or `example.com`. Unallowed characters include spaces and underscores.
    ```sh
    [a-z0-9]([-a-z0-9]*[a-z0-9])?(\.[a-z0-9]([-a-z0-9]*[a-z0-9])?)*
    ```
    {: screen}

* **Service credentials**: To use your existing service credentials, specify the `--key` flag in the `ibmcloud oc cluster service bind` command and provide the name of your service credentials. {{site.data.keyword.cloud_notm}} service binding automatically creates a Kubernetes secret with your existing service credentials.

### What if I want to use service credentials that use the private cloud service endpoint?
{: #svc-bind-private-cse}

By default, the `ibmcloud oc cluster service bind` command creates service credentials with the public cloud service endpoint. To use the private cloud service endpoint, you must manually create service credentials for your service that use the private cloud service endpoint, and then use the `--key` option to specify the name of the existing service credentials.  

Your service might not yet support private cloud service endpoints.

### Can I use all {{site.data.keyword.cloud_notm}} services in my cluster?
{: #svc-bind-which}

You can use service binding only for services that support service keys so that the service credentials can automatically be created and stored in a Kubernetes secret. To find a list of services that support service keys, see [Enabling external apps to use {{site.data.keyword.cloud_notm}} services](/docs/account?topic=account-externalapp#externalapp).

Services that don't support service keys usually provide an API that you can use in your app. The service binding method does not automatically set up API access for your app. Make sure to review the API documentation of your service and implement the API interface in your app.

### Can I bind multiple {{site.data.keyword.cloud_notm}} services to multiple clusters at once?
{: #svc-bind-trusted-profile}

{{site.data.keyword.cloud_notm}} service binding is on a per-cluster, per-service basis, and works by creating a Kubernetes secret that your pods can mount.

For multiple clusters and services, you can [use IAM trusted profiles instead](/docs/containers?topic=containers-pod-iam-identity). In IAM, you create a trusted profile with access policies for the {{site.data.keyword.cloud_notm}} services that you want. Then, you link the trusted profile with as many clusters as you want, based on conditions such as all the `prod` Kubernetes namespaces in clusters in a resource group. Finally, your pods mount the Kubernetes service account projected volume to get a token that can be exchanged for an IAM token that your apps use to authenticate with the {{site.data.keyword.cloud_notm}} services.

## Adding IBM Cloud services to clusters
{: #bind-services}

Use {{site.data.keyword.cloud_notm}} service binding to automatically create service credentials for your {{site.data.keyword.cloud_notm}} services and store these credentials in a Kubernetes secret.
{: shortdesc}

Before you begin:
- Ensure you have the following roles:
    - [**Editor** or **Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#checking-perms) for the cluster where you want to bind a service
    - [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-users#checking-perms) for the {{site.data.keyword.openshiftshort}} project where you want to bind the service
    - For Cloud Foundry services: [**Developer** Cloud Foundry role](/docs/account?topic=account-mngcf#mngcf) for the space where you want to provision the service
- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To add an {{site.data.keyword.cloud_notm}} service to your cluster:

1. [Create an instance of the {{site.data.keyword.cloud_notm}} service](/docs/account?topic=account-externalapp#externalapp).

    * Some {{site.data.keyword.cloud_notm}} services are available only in select regions. You can bind a service to your cluster only if the service is available in the same region as your cluster. In addition, if you want to create a service instance in the Washington DC zone, you must use the CLI.
    * **For IAM-enabled services**: You must create the service instance in the same resource group as your cluster. A service can be created in only one resource group that you can't change afterward.
    * Make sure that the service name is in the following regex format. Example permitted names are `myservice` or `example.com`. Unallowed characters include spaces and underscores.
        ```
        [a-z0-9]([-a-z0-9]*[a-z0-9])?(\.[a-z0-9]([-a-z0-9]*[a-z0-9])?)*
        ```
        {: screen}

2. Check the type of service that you created and make note of the service instance **Name**.
    - **Cloud Foundry services:**
        ```sh
        ibmcloud service list
        ```
        {: pre}

        Example output
        ```sh
        NAME                         service           plan    bound apps   last operation
        <cf_service_instance_name>   <service_name>    spark                create succeeded
        ```
        {: screen}

    - **{{site.data.keyword.cloud_notm}} IAM-enabled services:**
        ```sh
        ibmcloud resource service-instances
        ```
        {: pre}

        Example output
        ```sh
        NAME                          Location   State    Type               Tags
        <iam_service_instance_name>   <region>   active   service_instance
        ```
        {: screen}

    You can also see the different service types in your {{site.data.keyword.cloud_notm}} dashboard as **Cloud Foundry Services** and **Services**.

3. Identify the cluster project that you want to use to add your service.
    ```sh
    oc get namespaces
    ```
    {: pre}

4. Bind the service to your cluster to create service credentials for your service that use the public cloud service endpoint and store the credentials in a Kubernetes secret. If you have existing service credentials, use the `--key` flag to specify the name of the credentials. For IAM-enabled services, the credentials are automatically created with the **Writer** service access role, but you can use the `--role` flag to specify a different service access role. If you use the `--key` flag, don't include the `--role` flag.

    If your service supports private cloud service endpoints, you can manually create the service credentials with the private cloud service endpoint, and then use the `--key` flag to specify the name of your credentials.
    {: tip}

    ```sh
    ibmcloud oc cluster service bind --cluster <cluster_name_or_ID> --namespace <project> --service <service_instance_name> [--key <service_instance_key>] [--role <IAM_service_role>]
    ```
    {: pre}

    When the creation of the service credentials is successful, a Kubernetes secret with the name `binding-<service_instance_name>` is created.  

    Example output

    ```sh
    ibmcloud oc cluster service bind --cluster mycluster --namespace myproject --service cleardb
    Binding service instance to namespace...
    OK
    Namespace:         myproject
    Secret name:     binding-<service_instance_name>
    ```
    {: screen}

5. Verify the service credentials in your Kubernetes secret.
    1. Get the details of the secret and note the **binding** value. The **binding** value is base64 encoded and holds the credentials for your service instance in JSON format.
        ```sh
        oc get secrets binding-<service_instance_name> --namespace=<project> -o yaml
        ```
        {: pre}

        Example output
        ```yaml
        apiVersion: v1
        data:
        binding: <binding>
        kind: Secret
        metadata:
          annotations:
            service-instance-id: 1111aaaa-a1aa-1aa1-1a11-111aa111aa11
            service-key-id: 2b22bb2b-222b-2bb2-2b22-b22222bb2222
          creationTimestamp: 2018-08-07T20:47:14Z
          name: binding-<service_instance_name>
          namespace: <project>
          resourceVersion: "6145900"
          selfLink: /api/v1/namespaces/default/secrets/binding-mycloudant
          uid: 33333c33-3c33-33c3-cc33-cc33333333c
        type: Opaque
        ```
        {: screen}

    2. Decode the binding value.
        ```sh
        echo "<binding>" | base64 -D
        ```
        {: pre}

        Example output
        ```sh
        {"apikey":"<API_key>","host":"<ID_string>-bluemix.cloudant.com","iam_apikey_description":"Auto generated apikey during resource-key operation for Instance - crn:v1:bluemix:public:cloudantnosqldb:us-south:a/<ID_string>::","iam_apikey_name":"auto-generated-apikey-<ID_string>","iam_role_crn":"crn:v1:bluemix:public:iam::::serviceRole:Writer","iam_serviceid_crn":"crn:v1:bluemix:public:iam-identity::a/1234567890brasge5htn2ec098::serviceid:ServiceId-<ID_string>","password":"<ID_string>","port":443,"url":"https://<ID_string>-bluemix.cloudant.com","username":"123b45da-9ce1-4c24-ab12-rinwnwub1294-bluemix"}
        ```
        {: screen}

    3. Optional: Compare the service credentials that you decoded in the previous step with the service credentials that you find for your service instance in the {{site.data.keyword.cloud_notm}} dashboard.

6. Now that your service is bound to your cluster, you must configure your app to [access the service credentials in the Kubernetes secret](#adding_app).

## Accessing service credentials from your apps
{: #adding_app}

To access an {{site.data.keyword.cloud_notm}} service instance from your app, you must make the service credentials that are stored in the Kubernetes secret available to your app.
{: shortdesc}

The credentials of a service instance are base64 encoded and stored inside your secret in JSON format. To access the data in your secret, choose among the following options:
- [Mount the secret as a volume to your pod](#mount_secret)
- [Reference the secret in environment variables](#reference_secret)

Before you begin:
-  Ensure you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-users#checking-perms) for the `kube-system` project.
- [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
- [Add an {{site.data.keyword.cloud_notm}} service to your cluster](#bind-services).

### Mounting the secret as a volume to your pod
{: #mount_secret}

When you mount the secret as a volume to your pod, a file that is named `binding` is stored in the volume mount directory. The `binding` file in JSON format includes all the information and credentials that you need to access the {{site.data.keyword.cloud_notm}} service.
{: shortdesc}

1. List available secrets in your cluster and note the **name** of your secret. Look for a secret of type **Opaque**. If multiple secrets exist, contact your cluster administrator to identify the correct service secret.
    ```sh
    oc get secrets
    ```
    {: pre}

    Example output

    ```sh
    NAME                              TYPE            DATA      AGE
    binding-<service_instance_name>   Opaque          1         3m
    ```
    {: screen}

2. Create a YAML file for your Kubernetes deployment and mount the secret as a volume to your pod.
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      labels:
        app: secret-test
      name: secret-test
      namespace: <my_project>
    spec:
      selector:
        matchLabels:
          app: secret-test
      replicas: 1
      template:
        metadata:
          labels:
            app: secret-test
        spec:
          containers:
          - image: icr.io/ibm/liberty:latest
            name: secret-test
            volumeMounts:
            - mountPath: <mount_path>
              name: <volume_name>
          volumes:
          - name: <volume_name>
            secret:
              defaultMode: 420
              secretName: binding-<service_instance_name>
    ```
    {: codeblock}

    `volumeMounts.mountPath`
    :   The absolute path of the directory to where the volume is mounted inside the container.
    
    `volumeMounts.name` and `volumes.name`
    :   The name of the volume to mount to your pod.
    
    `secret.defaultMode`
    :   The read and write permissions on the secret. Use `420` to set read-only permissions.
    
    `secret.secretName`
    :   The name of the secret that you noted in the previous step.

3. Create the pod and mount the secret as a volume.
    ```sh
    oc apply -f secret-test.yaml
    ```
    {: pre}

4. Verify that the pod is created.
    ```sh
    oc get pods
    ```
    {: pre}

    Example CLI output:

    ```sh
    NAME                           READY     STATUS    RESTARTS   AGE
    secret-test-1111454598-gfx32   1/1       Running   0          1m
    ```
    {: screen}

5. Access the service credentials.
    1. Log in to your pod.
        ```sh
        oc exec <pod_name> -it bash
        ```
        {: pre}

    2. Navigate to your volume mount path that you defined earlier and list the files in your volume mount path.
        ```sh
        cd <volume_mountpath> && ls
        ```
        {: pre}

        Example output
        ```sh
        binding
        ```
        {: screen}

        The `binding` file includes the service credentials that you stored in the Kubernetes secret.

    3. View the service credentials. The credentials are stored as key value pairs in JSON format.
        ```sh
        cat binding
        ```
        {: pre}

        Example output
        ```sh
        {"apikey":"<API_key>","host":"<ID_string>-bluemix.cloudant.com","iam_apikey_description":"Auto generated apikey during resource-key operation for Instance - crn:v1:bluemix:public:cloudantnosqldb:us-south:a/<ID_string>:<ID_string>::","iam_apikey_name":"auto-generated-apikey-<ID_string>","iam_role_crn":"crn:v1:bluemix:public:iam::::serviceRole:Writer","iam_serviceid_crn":"crn:v1:bluemix:public:iam-identity::a/<ID_string>::serviceid:ServiceId-<ID_string>","password":"<ID_string>","port":443,"url":"https://<ID_string>-bluemix.cloudant.com","username":"123b45da-9ce1-4c24-ab12-rinwnwub1294-bluemix"}
        ```
        {: screen}

    4. Configure your app to parse the JSON content and retrieve the information that you need to access your service.

### Referencing the secret in environment variables
{: #reference_secret}

You can add the service credentials and other key value pairs from your Kubernetes secret as environment variables to your deployment.
{: shortdesc}

1. List available secrets in your cluster and note the **name** of your secret. Look for a secret of type **Opaque**. If multiple secrets exist, contact your cluster administrator to identify the correct service secret.
    ```sh
    oc get secrets
    ```
    {: pre}

    Example output

    ```sh
    NAME                              TYPE            DATA      AGE
    binding-<service_instance_name>   Opaque          1         3m
    ```
    {: screen}

2. Get the details of your secret to find potential key value pairs that you can reference as environment variables in your pod. The service credentials are stored in the `binding` key of your secret.
    ```sh
    oc get secrets binding-<service_instance_name> --namespace=<project> -o yaml
    ```
    {: pre}

    Example output

    ```yaml
    apiVersion: v1
    data:
      binding: <binding>
    kind: Secret
    metadata:
      annotations:
        service-instance-id: 7123acde-c3ef-4ba2-8c52-439ac007fa70
        service-key-id: 9h30dh8a-023f-4cf4-9d96-d12345ec7890
      creationTimestamp: 2018-08-07T20:47:14Z
      name: binding-<service_instance_name>
      namespace: <project>
      resourceVersion: "6145900"
      selfLink: /api/v1/namespaces/default/secrets/binding-mycloudant
      uid: 12345a31-9a83-11e8-ba83-cd49014748f
    type: Opaque
    ```
    {: screen}

3. Create a YAML file for your Kubernetes deployment and specify an environment variable that references the `binding` key.

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      labels:
        app: secret-test
      name: secret-test
      namespace: <my_project>
    spec:
      selector:
        matchLabels:
          app: secret-test
      template:
        metadata:
          labels:
            app: secret-test
        spec:
          containers:
          - image: icr.io/ibm/liberty:latest
            name: secret-test
            env:
            - name: BINDING
              valueFrom:
                secretKeyRef:
                  name: binding-<service_instance_name>
                  key: binding
    ```
    {: codeblock}

    `containers.env.name`
    :   The name of your environment variable.
    
    `env.valueFrom.secretKeyRef.name`
    :   The name of the secret that you noted in the previous step.
    
    `env.valueFrom.secretKeyRef.key`
    :   The key that is part of your secret and that you want to reference in your environment variable. To reference the service credentials, you must use the **binding** key.

4. Create the pod that references the `binding` key of your secret as an environment variable.
    ```sh
    oc apply -f secret-test.yaml
    ```
    {: pre}

5. Verify that the pod is created.
    ```sh
    oc get pods
    ```
    {: pre}

    Example CLI output:
    ```sh
    NAME                           READY     STATUS    RESTARTS   AGE
    secret-test-1111454598-gfx32   1/1       Running   0          1m
    ```
    {: screen}

6. Verify that the environment variable is set correctly.
    1. Log in to your pod.
        ```sh
        oc exec <pod_name> -it bash
        ```
        {: pre}

    2. List all environment variables in the pod.
        ```sh
        env
        ```
        {: pre}

        Example output
        ```sh
        BINDING={"apikey":"<API_key>","host":"<ID_string>-bluemix.cloudant.com","iam_apikey_description":"Auto generated apikey during resource-key operation for Instance - crn:v1:bluemix:public:cloudantnosqldb:us-south:a/<ID_string>::","iam_apikey_name":"auto-generated-apikey-<ID_string>","iam_role_crn":"crn:v1:bluemix:public:iam::::serviceRole:Writer","iam_serviceid_crn":"crn:v1:bluemix:public:iam-identity::a/1234567890brasge5htn2ec098::serviceid:ServiceId-<ID_string>","password":"<password>","port":443,"url":"https://<ID_string>-bluemix.cloudant.com","username":"<ID_string>-bluemix"}
        ```
        {: screen}

7. Configure your app to read the environment variable and to parse the JSON content to retrieve the information that you need to access your service.

    Example code in Python:
    ```python
    if os.environ.get('BINDING'):
        credentials = json.loads(os.environ.get('BINDING'))
    ```
    {: codeblock}

8. Optional: As a precaution, add error handling to your app in case that the `BINDING` environment variable is not set properly.

    Example code in Java:
    ```java
    if (System.getenv("BINDING") == null) {
    throw new RuntimeException("Environment variable 'SECRET' is not set!");
    }
    ```
    {: codeblock}

    Example code in Node.js:
    ```js
    if (!process.env.BINDING) {
    console.error('ENVIRONMENT variable "BINDING" is not set!');
    process.exit(1);
    }
    ```
    {: codeblock}

## Removing a service from a cluster
{: #unbind-service}

If you don't want to use an {{site.data.keyword.cloud_notm}} service that you bound to your cluster, you can manually remove the Kubernetes secret and the pods that access the secret from your cluster.
{: shortdesc}

1. List the services that are bound to your cluster and note the name of your service and the project that the service is bound to.
    ```sh
    ibmcloud oc cluster service ls --cluster
    ```
    {: pre}

    Example output

    ```sh
    OK
    Service   Instance GUID                          Key                                                                  Namespace   
    myservice 12345ab1-1234-1abc-a12b-12abc12a12ab   kube-a1a12abcd12a123abc1a12ab1a1234ab7.abcdefg0p1abcd123lgg.default   default  
    ```
    {: screen}

2. List the Kubernetes secrets in the project that your service is bound to and look for the secret with a name that follows the `binding-<service_name>` format.
    ```sh
    oc get secrets -n <project> | grep Opaque
    ```
    {: pre}

    Example output

    ```sh
    binding-myservice   Opaque     1      3d23h
    ```
    {: screen}

3. Retrieve all the pods that access the secret.
    ```sh
    oc get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.volumes[*]}{.secret.secretName}{" "}{end}{end}' | grep "<secret_name>"
    ```
    {: pre}

    If your CLI output is empty, no pods exist in your cluster that mount the secret.

4. If you have pods that mount the secret, either remove the pod or the deployment that manages the pod, or update the pod and deployment YAML to use a different secret instead.
    - **To remove a pod or deployment**:
        ```sh
        oc delete pod <pod_name> -n <project>
        ```
        {: pre}

        ```sh
        oc delete deployment <deployment_name> -n <project>
        ```
        {: pre}

    - **To update an existing pod or deployment**:
        1. Get the pod or deployment YAML file.
            ```sh
            oc get pod <pod_name> -o yaml
            ```
            {: pre}

            ```sh
            oc get deployment <deployment_name> -o yaml
            ```
            {: pre}

        2. Copy the YAML file and in the `spec.volumes` section, change the name of the secret that you want to use.
        3. Apply the change in your cluster.
            ```sh
            oc apply -f pod.yaml
            ```
            {: pre}

            ```sh
            oc apply -f deployment.yaml
            ```
            {: pre}

        4. Verify that a new pod is created with the updated volume specification.
            ```sh
            oc get pods
            ```
            {: pre}

            ```sh
            oc describe pod <pod_name>
            ```
            {: pre}

5. Remove the secret.
    ```sh
    oc delete secret <secret_name> -n <project>
    ```
    {: pre}

6. Verify that your secret is removed.
    ```sh
    oc get secrets -n <project>
    ```
    {: pre}

7. Optional. Remove the {{site.data.keyword.cloud_notm}} service instance.
    - **{{site.data.keyword.cloud_notm}} IAM-enabled services:**
        ```sh
        ibmcloud resource service-instance-delete <service_name>
        ```
        {: pre}

    - **Cloud Foundry services:**
        ```sh
        ibmcloud service delete <service_name>
        ```
        {: pre}




