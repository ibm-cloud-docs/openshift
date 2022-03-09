---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-09"

keywords: file, debug, help

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Debugging Portworx failures
{: #debug_storage_px}
{: troubleshoot}
{: support}

Review the options to debug Portworx and find the root causes of any failures.
{: shortdesc}

## Checking whether the pod that mounts your storage instance is successfully deployed
{: #debug_storage_px_deploy}

Follow the steps to review any error messages related to pod deployment.
{: shortdesc}

1. List the pods in your cluster. A pod is successfully deployed if the pod shows a status of **Running**.

    ```sh
    oc get pods
    ```
    {: pre}

1. Get the details of your pod and review any error messages that are displayed in the **Events** section of your CLI output.

    ```sh
    oc describe pod <pod_name>
    ```
    {: pre}

1. Retrieve the logs for your pod and review any error messages.

    ```sh
    oc logs <pod_name>
    ```
    {: pre}
    

4. [Review the Portworx troubleshooting documentation for steps to resolve common errors](/docs/openshift?topic=openshift-sitemap#sitemap_portworx_storage).  

## Restarting your app pod
{: #debug_storage_px_restart}

Some issues can be resolved by restarting and redeploying your pods. Follow the steps to redeploy a specific pod.
{: shortdesc}

1. If your pod is part of a deployment, delete the pod and let the deployment rebuild it. If your pod is not part of a deployment, delete the pod and reapply your pod configuration file.
    1. Delete the pod.
        ```sh
        oc delete pod <pod_name>
        ```
        {: pre}

        Example output
        ```sh
        pod "nginx" deleted
        ```
        {: screen}

    2. Reapply the configuration file to redeploy the pod.
        ```sh
        oc apply -f <app.yaml>
        ```
        {: pre}

        Example output
        ```sh
        pod/nginx created
        ```
        {: pre}

1. If restarting your pod does not resolve the issue, [reload your worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload).

1. Verify that you use the latest {{site.data.keyword.cloud_notm}} and {{site.data.keyword.containerlong_notm}} plug-in version.

    ```sh
    ibmcloud update
    ```
    {: pre}

    ```sh
    ibmcloud plugin repo-plugins
    ```
    {: pre}

    ```sh
    ibmcloud plugin update
    ```
    {: pre}
    

## Verifying that the Portworx storage driver and plug-in pods show a status of **Running**
{: #debug_storage_px_driver_plugin}

Follow the steps to check the status of your storage driver and plug-in pods and review any error messages.
{: shortdesc}

1. List the pods in the `kube-system` project.
    ```sh
    oc get pods -n kube-system | grep `portworx\|stork` 
    ```
    {: pre}

    Example output:
    ```
    portworx-594rw                          1/1       Running     0          20h
    portworx-rn6wk                          1/1       Running     0          20h
    portworx-rx9vf                          1/1       Running     0          20h
    stork-6b99cf5579-5q6x4                  1/1       Running     0          20h
    stork-6b99cf5579-slqlr                  1/1       Running     0          20h
    stork-6b99cf5579-vz9j4                  1/1       Running     0          20h
    stork-scheduler-7dd8799cc-bl75b         1/1       Running     0          20h
    stork-scheduler-7dd8799cc-j4rc9         1/1       Running     0          20h
    stork-scheduler-7dd8799cc-knjwt         1/1       Running     0          20h
    ```
    {: screen}

1. If the storage driver and plug-in pods don't show a **Running** status, get more details of the pod to find the root cause. Depending on the status of your pod, you might not be able to execute all the following commands.
    1. Get the names of the containers that run in the driver pod.
        ```sh
        kubectl describe pod <pod_name> -n kube-system 
        ```
        {: pre}

    2. Export the logs from the driver pod to a `logs.txt` file on your local machine. 
        ```sh
        oc logs <pod_name> -n kube-system > logs.txt
        ```
        {: pre}

    3. Review the log file.
        ```sh
        cat logs.txt
        ```
        {: pre} 

3. Check the latest logs for any error messages. [Review the Portworx troubleshooting documentation for steps to resolve common errors](/docs/openshift?topic=openshift-sitemap#sitemap_portworx_storage).

## Checking and updating the oc CLI version
{: #debug_storage_px_cli}

If you use a `oc` CLI version that does not match at least the major.minor version of your cluster, you might experience unexpected results. For example, [Kubernetes does not support](https://kubernetes.io/releases/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).
{: shortdesc}

1. Verify that the `oc` CLI version that you run on your local machine matches the Kubernetes version that is installed in your cluster. Show the `oc` CLI version that is installed in your cluster and your local machine.
    ```sh
    oc version
    ```
    {: pre}

    Example output:
    ```sh
    Client Version: version.Info{Major:"1", Minor:"23", GitVersion:"v1.22.7", GitCommit:"641856db18352033a0d96dbc99153fa3b27298e5", GitTreeState:"clean", BuildDate:"2019-03-25T15:53:57Z", GoVersion:"go1.12.1", Compiler:"gc", Platform:"darwin/amd64"}
    Server Version: version.Info{Major:"1", Minor:"23", GitVersion:"v1.22.7+IKS", GitCommit:"e15454c2216a73b59e9a059fd2def4e6712a7cf0", GitTreeState:"clean", BuildDate:"2019-04-01T10:08:07Z", GoVersion:"go1.11.5", Compiler:"gc", Platform:"linux/amd64"}
    ```   
    {: screen}

    The CLI versions match if you can see the same version in `GitVersion` for the client and the server. You can ignore the `+IKS` part of the version for the server.

2. If the `oc` CLI versions on your local machine and your cluster don't match, either [update your cluster](/docs/openshift?topic=openshift-update) or [install a different CLI version on your local machine](/docs/openshift?topic=openshift-openshift-cli#cs_cli_upgrade).

## Updating Helm charts
{: #debug_storage_px_helm}

1. Find the [latest Helm chart version](https://github.com/IBM/charts/tree/master/community/portworx){: external}.

2. List the installed Helm charts in your cluster and compare the version that you installed with the latest version.

    ```sh
    helm list --all-namespaces
    ```
    {: pre}



3. If a more recent version is available, install the new version. For instructions, see [Updating Portworx in your cluster](/docs/openshift?topic=openshift-portworx#update_portworx)(/docs/openshift?topic=openshift-portworx#update_portworx).





