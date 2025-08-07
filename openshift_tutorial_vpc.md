---

copyright:
  years: 2014, 2025
lastupdated: "2025-08-07"


keywords: kubernetes, openshift, red hat, red hat openshift

subcollection: openshift

content-type: tutorial
services: openshift, vpc
account-plan:
completion-time: 45m

---

{{site.data.keyword.attribute-definition-list}}





# Setting up your first cluster in your Virtual Private Cloud (VPC)
{: #vpc_rh_tutorial}
{: toc-content-type="tutorial"}
{: toc-services="openshift, vpc"}
{: toc-completion-time="45m"}

[Virtual Private Cloud]{: tag-vpc} 

Create an {{site.data.keyword.openshiftlong}} cluster in your Virtual Private Cloud (VPC).
{: shortdesc}

- {{site.data.keyword.openshiftlong_notm}} gives you all the [advantages of a managed offering](/docs/openshift?topic=openshift-overview) for your cluster infrastructure environment, while using the [{{site.data.keyword.redhat_openshift_notm}} tooling and catalog](https://docs.redhat.com/documentation/openshift_container_platform/4.18/html/about/welcome-index){: external} that runs on Red Hat Enterprise Linux for your app deployments.
- VPC gives you the security of a private cloud environment with the dynamic scalability of a public cloud. VPC uses the next version of {{site.data.keyword.openshiftlong_notm}} [infrastructure providers](/docs/openshift?topic=openshift-overview#what-compute-infra-is-offered), with a select group of v2 API, CLI, and console functionality.

## Audience
{: #vpc_rh_audience}

This tutorial is for administrators who are creating a cluster in {{site.data.keyword.openshiftlong_notm}} in VPC compute for the first time.
{: shortdesc}

## Objectives
{: #vpc_rh_objectives}

In the tutorial lessons, you create a {{site.data.keyword.openshiftlong_notm}} cluster in a Virtual Private Cloud (VPC). Then, you access built-in {{site.data.keyword.redhat_openshift_notm}} components, deploy an app in a {{site.data.keyword.redhat_openshift_notm}} project, and expose the app with a VPC load balancer so that external users can access the service.

## What you'll get
{: #vpc_rh_get}

In this tutorial, you will create the following resources. There are optional steps to delete these resources if you do not want to keep them after completing the tutorial. 

- A VPC cluster
- A simple Hello World app deployed to your cluster
- A VPC load balancer to expose your app


## Prerequisites
{: #vpc_rh_prereqs}

Complete the following prerequisite steps to set up permissions and the command-line environment.
{: shortdesc}

**Permissions**: If you are the account owner, you already have the required permissions to create a cluster and can continue to the next step. Otherwise, ask the account owner to [set up the API key and assign you the minimum user permissions in {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-iam-platform-access-roles).

**Command-line tools**: For quick access to your resources from the command line, try the [{{site.data.keyword.cloud-shell_notm}}](https://cloud.ibm.com/shell){: external}. Otherwise, set up your local command-line environment by completing the following steps.
1. [Install the {{site.data.keyword.cloud_notm}} CLI (`ibmcloud`), {{site.data.keyword.containershort_notm}} plug-in (`ibmcloud oc`), and {{site.data.keyword.registrylong_notm}} plug-in (`ibmcloud cr`)](/docs/openshift?topic=openshift-cli-install).
2. [Install the {{site.data.keyword.redhat_openshift_notm}} (`oc`) and Kubernetes (`kubectl`) CLIs](/docs/openshift?topic=openshift-cli-install).
3. To work with VPC, install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}

4. Update your {{site.data.keyword.containershort_notm}} plug-in to the latest version.
    ```sh
    ibmcloud plugin update kubernetes-service
    ```
    {: pre}



## Create a cluster in a VPC
{: #vpc_rh_create_vpc_cluster}
{: step}

Create an {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) environment. Then, create a {{site.data.keyword.openshiftlong_notm}} cluster on the VPC infrastructure. For more information about VPC, see [Getting Started with Virtual Private Cloud](/docs/vpc?topic=vpc-getting-started).
{: shortdesc}

1. Log in to the account, resource group, and {{site.data.keyword.cloud_notm}} region where you want to create your VPC environment. The VPC must be set up in the same multizone metro region where you want to create your cluster. In this tutorial you create a VPC in `us-south`. For other supported regions, see [Multizone metros for VPC clusters](/docs/openshift?topic=openshift-regions-and-zones). If you have a federated ID, include the `--sso` option.
    ```sh
    ibmcloud login -r us-south [-g <resource_group>] [--sso]
    ```
    {: pre}

2. Create a VPC for your cluster. For more information, see the docs for creating a VPC in the [console](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console) or [CLI](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli).
    1. Create a VPC called `myvpc` and note the **ID** in the output. VPCs provide an isolated environment for your workloads to run within the public cloud. You can use the same VPC for multiple clusters, such as if you plan to have different clusters host separate microservices that need to communicate with each other. If you want to separate your clusters, such as for different departments, you can create a VPC for each cluster.
        ```sh
        ibmcloud is vpc-create myvpc
        ```
        {: pre}

    2. Create a public gateway and note the **ID** in the output. In the next step, you attach the public gateway to a VPC subnet, so that your worker nodes can communicate on the public network. Default {{site.data.keyword.redhat_openshift_notm}} components, such as the web console and OperatorHub, require public network access. If you skip this step, you must instead be connected to your VPC private network, such as through a VPN connection, to access the {{site.data.keyword.redhat_openshift_notm}} web console or access your cluster with `kubectl` commands.
        ```sh
        ibmcloud is public-gateway-create gateway-us-south-1 <vpc_ID> us-south-1
        ```
        {: pre}

    3. Create a subnet for your VPC, and note its **ID**. Consider the following information when you create the VPC subnet:
        *  **Zones**: You must have one VPC subnet for each zone in your cluster. The available zones depend on the region that you created the VPC in. To list available zones in the region, run `ibmcloud is zones`.
        *  **IP addresses**: VPC subnets provide private IP addresses for your worker nodes and load balancer services in your cluster, so make sure to [create a subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IP addresses that a VPC subnet has later.
        *  **Public gateways**: Include the public gateway that you previously created. You must have one public gateway for each zone in your cluster.

            ```sh
            ibmcloud is subnet-create mysubnet1 <vpc_ID> --zone us-south-1 --ipv4-address-count 256 --pgw <gateway_ID>
            ```
            {: pre}
    
    If you have multiple zones, repeat these steps for each zone.
    {: tip}

3. Create a standard {{site.data.keyword.cos_full_notm}} instance to back up the internal registry in your cluster. In the output, note the instance **ID**.
    ```sh
    ibmcloud resource service-instance-create myvpc-cos cloud-object-storage standard global
    ```
    {: pre}

4. Create a cluster in your VPC in the same zone as the subnet.
    The following command creates a version 4.18 cluster in Dallas with the minimum configuration of 2 worker nodes that have at least 4 cores and 16 GB memory so that default {{site.data.keyword.redhat_openshift_notm}} components can deploy. For more information about the command options, see the [`cluster create vpc-gen2` CLI reference docs](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_cluster-create-vpc-gen2).
    ```sh
    ibmcloud oc cluster create vpc-gen2 --name myvpc-cluster --zone us-south-1 --version 4.18_openshift --flavor bx2.4x16 --workers 2 [--operating-system REDHAT_8_64] --vpc-id <vpc_ID> --subnet-id <vpc_subnet_ID> --cos-instance <cos_crn> --disable-outbound-traffic-protection
    ```
    {: pre}

5. List your cluster details. Review the cluster **State**, check the **Ingress Subdomain**, and note the **Master URL**.
    Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and Ingress components take about 10 more minutes to deploy and update the cluster domain that you use for the {{site.data.keyword.redhat_openshift_notm}} web console and other routes. Before you continue, wait until the cluster is ready by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.
    {: note}
    
    ```sh
    ibmcloud oc cluster get --cluster myvpc-cluster
    ```
    {: pre}

6. Add yourself as a user to the {{site.data.keyword.redhat_openshift_notm}} cluster by setting the cluster context.
    ```sh
    ibmcloud oc cluster config --cluster myvpc-cluster --admin
    ```
    {: pre}

7. In your browser, navigate to the address of your **Master URL** and append `/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`. If time permits, you can explore the different areas of the {{site.data.keyword.redhat_openshift_notm}} web console.
    
8. From the {{site.data.keyword.redhat_openshift_notm}} web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate via the CLI.
    
    Save your cluster master URL to access the {{site.data.keyword.redhat_openshift_notm}} console later. In future sessions, you can skip the `cluster config` step and copy the login command from the console instead.
    {: tip}
    
9. Verify that the `oc` commands run properly with your cluster by checking the version.
    ```sh
    oc version
    ```
    {: pre}

    Example output

    ```sh
    Client Version: v4.18.0
    Kubernetes Version: v1.32.7.2
    ```
    {: screen}

    If you can't perform operations that require Administrator permissions, such as listing all the worker nodes or pods in a cluster, download the TLS certificates and permission files for the cluster administrator by running the `ibmcloud oc cluster config --cluster myvpc-cluster --admin` command.
    {: tip}



## Deploy an app to your cluster
{: #vpc_rh_app}
{: step}

Quickly deploy a new sample app that is available to requests from inside the cluster only.
{: shortdesc}

1. Create a {{site.data.keyword.redhat_openshift_notm}} project for your Hello World app.
    ```sh
    oc new-project hello-world
    ```
    {: pre}

2. Build the sample app [from the source code](https://github.com/IBM/container-service-getting-started-wt){: external}. With the {{site.data.keyword.redhat_openshift_notm}} `new-app` command, you can refer to a directory in a remote repository that contains the Dockerfile and app code to build your image. The command builds the image, stores the image in the local Docker registry, and creates the app deployment configurations (`dc`) and services (`svc`). For more information about creating new apps, [see the {{site.data.keyword.redhat_openshift_notm}} docs](https://docs.redhat.com/documentation/openshift_container_platform/4.18/html/building_applications/creating-applications){: external}.
    ```sh
    oc new-app --name hello-world https://github.com/IBM/container-service-getting-started-wt --context-dir="Lab 1"
    ```
    {: pre}

3. Verify that the sample Hello World app components are created.

    1. List the **hello-world** services and note the service name. So far, your app listens for traffic on these internal cluster IP addresses only. In the next lesson, you create a load balancer for the service so that the load balancer can forward external traffic requests to the app.
        ```sh
        oc get svc -n hello-world
        ```
        {: pre}

        Example output
        ```sh
        NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
        hello-world   ClusterIP   172.21.xxx.xxx   <none>       8080/TCP   31m
        ```
        {: screen}

    2. List the pods. Pods with `build` in the name are jobs that **Completed** as part of the new app build process. Make sure that the **hello-world** pod status is **Running**.
        ```sh
        oc get pods -n hello-world
        ```
        {: pre}

        Example output
        ```sh
        NAME                  READY     STATUS             RESTARTS   AGE
        hello-world-1-9cv7d   1/1       Running            0          30m
        hello-world-1-build   0/1       Completed          0          31m
        hello-world-1-deploy  0/1       Completed          0          31m
        ```
        {: screen}



## Set up a VPC load balancer to expose your app publicly
{: #vpc_rh_vpc_lb}
{: step}

Set up a VPC load balancer to expose your app to external requests on the public network.
{: shortdesc}

When you create a Kubernetes `LoadBalancer` service in your cluster, a VPC load balancer is automatically created in your VPC outside of your cluster. The VPC load balancer is multizonal and routes requests for your app through the private NodePorts that are automatically opened on your worker nodes. The following diagram illustrates how a user accesses an app's service through the VPC load balancer, even though your worker node is connected to only a private subnet.

1. Create a Kubernetes `LoadBalancer` service in your cluster to publicly expose the hello world app.
    ```sh
    oc expose deployment/hello-world --type=LoadBalancer --name=hw-lb-svc  --port=8080 --target-port=8080 -n hello-world
    ```
    {: pre}

    Example output

    ```sh
    service "hw-lb-svc" exposed
    ```
    {: screen}
    
    | Parameter | Description |
    | ------ | -------------- |
    | `expose` | Expose a Kubernetes resource, such as a deployment, as a service so that users can access the resource by using the VPC load balancer hostname. |
    | `dc/<hello-world-deployment>` | The resource type and the name of the resource to expose with this service. |
    | `--name=<hello-world-service>` | The name of the service. |
    | `--type=LoadBalancer` | The service type to create. In this lesson, you create a `LoadBalancer` service. |
    | `--port=<8080>` | The port on which the service listens for external network traffic. |
    | `--target-port=<8080>` | The port that your app listens on and to which the service directs incoming network traffic. In this example, the `target-port` is the same as the `port`, but other apps that you create might use a different port. |
    | `-n <hello-world>` | The namespace that your deployment is in. |
    {: caption="More about the expose parameters" caption-side="bottom"}

2. Verify that the Kubernetes `LoadBalancer` service is created successfully in your cluster. When you create the Kubernetes `LoadBalancer` service, a VPC load balancer is automatically created for you. The VPC load balancer assigns a hostname to your Kubernetes `LoadBalancer` service that you can see in the **LoadBalancer Ingress** field of your CLI output. In VPC, services in your cluster are assigned a hostname because the external IP address for the service is not stable.
    The VPC load balancer takes a few minutes to provision in your VPC. Until the VPC load balancer is ready, you can't access the Kubernetes `LoadBalancer` service through its hostname.
    {: note}

    ```sh
    oc describe service hw-lb-svc -n hello-world
    ```
    {: pre}

    Example CLI output:
    ```sh
    NAME:                     hw-lb-svc
    Namespace:                default
    Labels:                   app=hello-world-deployment
    Annotations:              <none>
    Selector:                 app=hello-world-deployment
    Type:                     LoadBalancer
    IP:                       172.21.xxx.xxx
    LoadBalancer Ingress:     1234abcd-us-south.lb.appdomain.cloud
    Port:                     <unset> 8080/TCP
    TargetPort:               8080/TCP
    NodePort:                 <unset> 32040/TCP
    Endpoints:
    Session Affinity:         None
    External Traffic Policy:  Cluster
    Events:
        Type    Reason                Age   From                Message
        ----    ------                ----  ----                -------
        Normal  EnsuringLoadBalancer  1m    service-controller  Ensuring load balancer
        Normal  EnsuredLoadBalancer   1m    service-controller  Ensured load balancer
    ```
    {: screen}

3. Verify that the VPC load balancer is created successfully in your VPC. In the output, verify that the VPC load balancer has a **Provision Status** of `active` and an **Operating Status** of `online`.

    The VPC load balancer is named in the format `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. To see your cluster ID, run `ibmcloud oc cluster get --cluster <cluster_name>`. To see the Kubernetes `LoadBalancer` service UID, run `kubectl get svc hw-lb-svc -o yaml` and look for the **metadata.uid** field in the output.
    {: tip}

    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

    In the following example CLI output, the VPC load balancer that is named `kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306` is created for the Kubernetes `LoadBalancer` service:
    ```sh
    ID                                          Name                                                         Family        Subnets               Is public   Provision status   Operating status   Resource group
    r006-d044af9b-92bf-4047-8f77-a7b86efcb923   kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306   Application   mysubnet-us-south-3   true        active             online             default
    ```
    {: screen}

4. Send a request to your app by curling the hostname and port of the Kubernetes `LoadBalancer` service that is assigned by the VPC load balancer that you found in step 2. Example:
    ```sh
    curl 1234abcd-us-south.lb.appdomain.cloud:8080
    ```
    {: pre}

    Example output

    ```sh
    Hello world from hello-world-deployment-5fd7787c79-sl9hn! Your app is up and running in a cluster!
    ```
    {: screen}

5. **Optional**: To clean up the resources that you created in this lesson, you can use the labels that are assigned to each app.
    1. List all the resources for each app in the `hello-world` project.
        ```sh
        oc get all -l app=hello-world -o name -n hello-world
        ```
        {: pre}

        Example output
        ```sh
        pod/hello-world-1-dh2ff
        replicationcontroller/hello-world-1
        service/hello-world
        deploymentconfig.apps.openshift.io/hello-world
        buildconfig.build.openshift.io/hello-world
        build.build.openshift.io/hello-world-1
        imagestream.image.openshift.io/hello-world
        imagestream.image.openshift.io/node
        ```
        {: screen}

    2. Delete all the resources that you created.
        ```sh
        oc delete all -l app=hello-world -n hello-world
        ```
        {: pre}



## What's next?
{: #vpc_rh_next}

Now that you have a VPC cluster, learn more about what you can do.
{: shortdesc}

- [Setting up block storage for your apps](/docs/openshift?topic=openshift-vpc-block)
- [Backing up your internal image registry to {{site.data.keyword.cos_full_notm}}](/docs/openshift?topic=openshift-registry#cos_image_registry)
- [VPC cluster limitations](/docs/openshift?topic=openshift-limitations#ks_vpc_gen2_limits)
- [About the v2 API](/docs/openshift?topic=openshift-cs_api_install#api_about)

Need help, have questions, or want to give feedback on VPC clusters? Try posting in the [Slack channel](https://ibm-cloud-success.slack.com/join/shared_invite/zt-2p5zqh275-FL8XUSEmn_vvAJZzrHqYcA){: external}.
{: tip}
