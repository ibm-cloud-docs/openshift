---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-14"

keywords: openshift, roks, rhoks, rhos, clusters

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Accessing OpenShift clusters
{: #access_cluster}
{: help}
{: support}

After your {{site.data.keyword.openshiftlong}} cluster is created, you can begin working with your cluster by accessing the cluster.
{: shortdesc}

## Prerequisites
{: #prereqs}

1. [Install the required CLI tools](/docs/openshift?topic=openshift-openshift-cli), including the {{site.data.keyword.cloud_notm}} CLI, {{site.data.keyword.containershort_notm}} plug-in alias for OpenShift (`ibmcloud oc`), and OpenShift CLI (`oc`).
2. [Create your OpenShift cluster](/docs/openshift?topic=openshift-clusters).
3. If your network is protected by a company firewall, [allow access](/docs/openshift?topic=openshift-firewall) to the {{site.data.keyword.cloud_notm}} and Red Hat OpenShift on IBM Cloud API endpoints and ports. For private service endpoint-only clusters, you cannot test the connection to your cluster until you expose the private service endpoint of the master to the cluster by using a [private NLB](#access_private_se).
4. Check that your cluster is in a healthy state by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`. If your cluster is not in a healthy state, review the [Debugging clusters](/docs/containers?topic=containers-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall).

<br />



## Accessing OpenShift clusters through the public service endpoint
{: #access_public_se}


For OpenShift clusters with a public service endpoint, you can get the `oc login` token by following the instructions in the console.
{: shortdesc}

1.  In the [Red Hat OpenShift on IBM Cloud console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the cluster that you want to access.
2.  Click the **Access** tab and follow the instructions.

<br />


## Accessing clusters through the private service endpoint
{: #access_private_se}

The OpenShift master is accessible through the private service endpoint if authorized cluster users are in your {{site.data.keyword.cloud_notm}} private network or are connected to the private network through a [VPN connection](/docs/infrastructure/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link). However, communication with the Kubernetes master over the private service endpoint must go through the <code>166.X.X.X</code> IP address range, which is not routable from a VPN connection or through {{site.data.keyword.cloud_notm}} Direct Link. You can expose the private service endpoint of the master for your cluster users by using a private network load balancer (NLB). The private NLB exposes the private service endpoint of the master as an internal <code>10.X.X.X</code> IP address range that users can access with the VPN or {{site.data.keyword.cloud_notm}} Direct Link connection. If you enable only the private service endpoint, you can use the Kubernetes dashboard or temporarily enable the public service endpoint to create the private NLB.
{: shortdesc}


1. Log in to your [OpenShift cluster](#access_public_se).

3. Get the private service endpoint URL and port for your cluster.
  ```
  ibmcloud oc cluster get --cluster <cluster_name_or_ID>
  ```
  {: pre}

  In this example output, the **Private Service Endpoint URL** is `https://c1.private.us-east.containers.cloud.ibm.com:31144`.
  ```
  Name:                           setest
  ID:                             b8dcc56743394fd19c9f3db7b990e5e3
  State:                          normal
  Created:                        2019-04-25T16:03:34+0000
  Location:                       wdc04
  Master URL:                     https://c1-e.us-east.containers.cloud.ibm.com:31144
  Public Service Endpoint URL:    https://c1-e.us-east.containers.cloud.ibm.com:31144
  Private Service Endpoint URL:   https://c1.private.us-east.containers.cloud.ibm.com:31144
  Master Location:                Washington D.C.
  ...
  ```
  {: screen}

4. Create a YAML file that is named `oc-api-via-nlb.yaml`. This YAML creates a private `LoadBalancer` service and exposes the private service endpoint through that NLB. Replace `<private_service_endpoint_port>` with the port you found in the previous step.
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: oc-api-via-nlb
    annotations:
      service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
    namespace: default
  spec:
    type: LoadBalancer
    ports:
    - protocol: TCP
      port: <private_service_endpoint_port>
      targetPort: <private_service_endpoint_port>
  ---
  kind: Endpoints
  apiVersion: v1
  metadata:
    name: oc-api-via-nlb
    namespace: default
  subsets:
    - addresses:
        - ip: 172.20.0.1
      ports:
        - port: 2040
  ```
  {: codeblock}

5. Create the NLB and endpoint.
   1. Apply the configuration file that you previously created.
      ```
      oc apply -f oc-api-via-nlb.yaml
      ```
      {: pre}
   1. Verify that the `oc-api-via-nlb` NLB is created. In the output, note the `10.x.x.x` **EXTERNAL-IP** address. This IP address exposes the private service endpoint for the cluster master on the port that you specified in your YAML file.
      ```
      oc get svc -o wide
      ```
      {: pre}

      In this example output, the IP address for the private service endpoint of the master is `10.186.92.42`.
      ```
      NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)          AGE   SELECTOR
      oc-api-via-nlb           LoadBalancer   172.21.150.118   10.186.92.42     443:32235/TCP    10m   <none>
      ...
      ```
      {: screen}

6. On the client machines where you or your users run `oc` commands, add the NLB IP address and the private service endpoint URL to the `/etc/hosts` file. Do not include any ports in the IP address and URL and do not include `https://` in the URL.
  * For OSX and Linux users:
    ```
    sudo nano /etc/hosts
    ```
    {: pre}
  * For Windows users:
    ```
    notepad C:\Windows\System32\drivers\etc\hosts
    ```
    {: pre}

    Depending on your local machine permissions, you might need to run Notepad as an administrator to edit the hosts file.
    {: tip}

    Example text to add:
    ```
    10.186.92.42      c1.private.us-east.containers.cloud.ibm.com
    ```
    {: codeblock}

7. [Create an API key](#access_api_key) with the private service endpoint so that you can log in to the cluster.

8. Verify that you are connected to the private network through a [VPN](/docs/infrastructure/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link) connection.

9.  Log in to the cluster with the API key. Include `https://` and the port in the private service endpoint URL, such as `https://c100.private.us-east.containers.cloud.ibm.com:30113`.
    ```
    oc login -u apikey -p <API_key> --server=<private_service_endpoint>
    ```
    {: pre}

10. Verify that the `oc` commands run properly with your cluster through the private service endpoint by checking the version.
    ```
    oc version
    ```
    {: pre}

    Example output:

    ```
    oc v3.11.0+0cbc58b
    kubernetes v1.11.0+d4cacc0
    features: Basic-Auth

    Server https://c1.private.us-east.containers.cloud.ibm.com:31144
    openshift v3.11.98
    kubernetes v1.11.0+d4cacc0
    ```
    {: screen}


<br />



## Accessing OpenShift clusters from automation tools by using an API key
{: #access_automation}

Red Hat OpenShift on IBM Cloud is integrated with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the OpenShift console, your IAM identity is used to generate an OpenShift login token that you can use to log in to the terminal. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the `oc login` command.
{:shortdesc}

### Using an API key to log in to OpenShift clusters
{: #access_api_key}

You can create an {{site.data.keyword.cloud_notm}} IAM API key and then use the API key to log in to an OpenShift cluster. With API keys, you can use the credentials of one user or shared account to access a cluster, instead of logging in individually. You might also create an API key for a [service ID](#access_service_id). For more information, see [Understanding API keys](/docs/iam?topic=iam-manapikey).
{: shortdesc}

1.  Create an {{site.data.keyword.cloud_notm}} API key.<p class="important">Save your API key in a secure location. You cannot retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` flag.</p>
    ```
    ibmcloud iam api-key-create <name>
    ```
    {: pre}
2.  Configure your cluster to add the API key user to your cluster RBAC policies and to set your session context to your cluster server.
    1.  Log in to {{site.data.keyword.cloud_notm}} with the API key credentials.
        ```
        ibmcloud login --apikey <API_key>
        ```
        {: pre}
    2.  Download the cluster configuration files.
        ```
        ibmcloud oc cluster-config --cluster <cluster_name_or_ID>
        ```
        {: pre}

        After downloading the configuration files, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable, such as the following example.
        ```
        export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/kubernetes-service/clusters/mycluster/kube-config-prod-dal10-mycluster.yml
        ```
        {: screen}
    3.  Copy and paste the command that is displayed in your terminal to set the `KUBECONFIG` environment variable.
3.  Use the API key to log in to your OpenShift cluster. The username (`-u`) is `apikey` and the password (`-p`) is your API key value.
    ```
    oc login -u apikey -p <API_key>
    ```
    {: pre}

    You can also use an API call to exchange your {{site.data.keyword.cloud_notm}} IAM credentials for an OpenShift token. To get the `master_URL`, run `ibmcloud oc cluster-get --cluster <cluster_name_or_ID>`. For more information, see the [OpenShift docs](https://docs.openshift.com/container-platform/3.11/architecture/additional_concepts/authentication.html#obtaining-oauth-tokens){: external}.

    Example curl request:
    ```
    curl -u 'apikey:<API_key>' -H "X-CSRF-Token: a" 'https://<master_URL>:<port>/oauth/authorize?client_id=openshift-challenging-client&response_type=token' -vvv
    ```
    {: pre}

### Using a service ID to log in to OpenShift clusters
{: #access_service_id}

You can create an {{site.data.keyword.cloud_notm}} IAM service ID, make an API key for the service ID, and then use the API key to log in to an OpenShift cluster. You might use service IDs so that apps that are hosted in other clusters or clouds can access your cluster's services. Because service IDs are not tied to a specific user, your apps can authenticate if individual users leave your account. For more information, see [Creating and working with service IDs](/docs/iam?topic=iam-serviceids).
{: shortdesc}

1.  Create an {{site.data.keyword.cloud_notm}} IAM service ID for your cluster that is used for the IAM policies and API key credentials. Be sure to give the service ID a description that helps you retrieve the service ID later, such as including the cluster name.
    ```
    ibmcloud iam service-id-create <cluster_name>-id --description "Service ID for Red Hat OpenShift on IBM Cloud cluster <cluster_name>"
    ```
    {: pre}

    Example output:
    ```
    Name          <cluster_name>-id   
    Description   Service ID for Red Hat OpenShift on IBM Cloud cluster <cluster_name>  
    CRN           crn:v1:bluemix:public:iam-identity::a/1aa111aa1a11111aaa1a1111aa1aa111::serviceid:ServiceId-bbb2b2b2-2bb2-2222-b222-b2b2b2222b22   
    Bound To      crn:v1:bluemix:public:::a/1aa111aa1a11111aaa1a1111aa1aa111:::   
    Version       1-c3c333333333ccccc33333c33cc3cc33   
    Locked        false   
    UUID          ServiceId-bbb2b2b2-2bb2-2222-b222-b2b2b2222b22
    ```
    {: screen}
2.  Create a custom {{site.data.keyword.cloud_notm}} IAM policy for your cluster service ID that grants access to Red Hat OpenShift on IBM Cloud.
    ```
    ibmcloud iam service-policy-create <cluster_service_ID> --service-name containers-kubernetes --roles <service_access_role> --service-instance <cluster_ID>
    ```
    {: pre}
    <table>
    <caption>Understanding this command's components</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code><em>&lt;cluster_service_ID&gt;</em></code></td>
    <td>Required. Enter the service ID that you previously created for your OpenShift cluster.</td>
    </tr>
    <tr>
    <td><code>--service-name <em>containers-kubernetes</em></code></td>
    <td>Required. Enter `containers-kubernetes` so that the IAM policy is for Red Hat OpenShift on IBM Cloud clusters.</td>
    </tr>
    <tr>
    <td><code>--roles <em>&lt;service_access_role&gt;</em></code></td>
    <td>Required. Enter the access role that you want the service ID to have to your OpenShift cluster. [Platform roles](/docs/openshift?topic=openshift-access_reference#iam_platform) permit cluster management activities such as creating worker nodes. [Service roles](/docs/openshift?topic=openshift-access_reference#service) correspond to RBAC roles that permit OpenShift management activities within the cluster, such as for Kubernetes resources like pods and namespaces. For multiple roles, include a comma-separated list. Possible values are `Administrator`, `Operator`, `Editor`, and `Viewer` (platform roles); and `Reader`, `Writer`, and `Manager` (service roles).</td>
    </tr>
    <tr>
      <td><code>--service-instance <em>&lt;cluster_ID&gt;</em></code></td>
      <td>To restrict the policy to a particular cluster, enter the cluster's ID. To get your cluster ID, run `ibmcloud oc clusters`.<p class="note">If you do not include the service instance, the access policy grants the service ID access to to all your {{site.data.keyword.containerlong_notm}} clusters, Kubernetes and OpenShift. You can also scope the access policy to a region (`--region`) or resource group (`--resource-group-name`).</td>
    </tr>
    </tbody></table>
3.  Create an API key for the service ID. Name the API key similar to your service ID, and include the service ID that you previously created, ``<cluster_name>-id`. Be sure to give the API key a description that helps you retrieve the key later.<p class="important">Save your API key in a secure location. You cannot retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` flag.</p>
    ```
    ibmcloud iam service-api-key-create <cluster_name>-key <service_ID> --description "API key for service ID <service_ID> in OpenShift cluster <cluster_name>"
    ```
    {: pre}

    Example output:
    ```
    Please preserve the API key! It cannot be retrieved after it's created.

    Name          <cluster_name>-key   
    Description   API key for service ID <service_ID> in OpenShift cluster <cluster_name>
    Bound To      crn:v1:bluemix:public:iam-identity::a/1bb222bb2b33333ddd3d3333ee4ee444::serviceid:ServiceId-ff55555f-5fff-6666-g6g6-777777h7h7hh   
    Created At    2019-02-01T19:06+0000   
    API Key       i-8i88ii8jjjj9jjj99kkkkkkkkk_k9-llllll11mmm1   
    Locked        false   
    UUID          ApiKey-222nn2n2-o3o3-3o3o-4p44-oo444o44o4o4   
    ```
    {: screen}
4.  Configure your cluster to add the service ID user to your cluster RBAC policies and to set your session context to your cluster server.
    1.  Log in to {{site.data.keyword.cloud_notm}} with the service ID's API key credentials.
        ```
        ibmcloud login --apikey <API_key>
        ```
        {: pre}
    2.  Download the cluster configuration files.
        ```
        ibmcloud oc cluster-config --cluster <cluster_name_or_ID>
        ```
        {: pre}

        After downloading the configuration files, a command is displayed that you can use to set the path to the local Kubernetes configuration file as an environment variable, such as the following example.
        ```
        export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/kubernetes-service/clusters/mycluster/kube-config-prod-dal10-mycluster.yml
        ```
        {: screen}
    3.  Copy and paste the command that is displayed in your terminal to set the `KUBECONFIG` environment variable.
5.  [Use the service ID's API key to log in to your OpenShift cluster](#access_api_key). The username (`-u`) is `apikey` and the password (`-p`) is your API key value.
    ```
    oc login -u apikey -p <API_key>
    ```
    {: pre}
6.  Verify that the service ID can perform the actions that you authorized.

    Example: If you assigned a `Reader` service role, the service ID can list pods in your OpenShift project.
    ```
    oc get pods
    ```
    {: pre}

    Example: If you assigned a `Manager` service role, the service ID can list the users in your OpenShift cluster. The ID of your IAM service ID is in the **Identities** output. Other individual users might be identified by their email address and IBMid.
    ```
    oc get users
    ```
    {: pre}

    Example output:
    ```
    NAME                           UID                                    FULL NAME   IDENTITIES
    IAM#                           dd44ddddd-d4dd-44d4-4d44-4d44d444d444              IAM:iam-ServiceId-bbb2b2b2-2bb2-2222-b222-b2b2b2222b22
    IAM#first.last@email.com       55555ee5-e555-55e5-e5e5-555555ee55ee               IAM:IBMid-666666FFF6
    ```
    {: screen}




