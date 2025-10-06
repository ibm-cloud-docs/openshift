---
copyright:
  years: 2014, 2025
lastupdated: "2025-10-06"


keywords: openshift, file, debug, help

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Debugging OpenShift Data Foundation failures
{: #debug_storage_ocs}
{: troubleshoot}
{: support}

Review the options to debug ODF and find the root causes of any failures.
{: shortdesc}

## Checking whether the pod that mounts your storage instance is successfully deployed
{: #debug_storage_ocs_deploy}

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
    

1. [Review the ODF troubleshooting documentation for steps to resolve common errors](/docs/openshift?topic=openshift-sitemap#sitemap_openshift_data_foundation).  

## Restarting your app pod
{: #debug_storage_ocs_restart}

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
    

## Verifying that the storage driver and plug-in pods show a status of **Running**
{: #debug_storage_ocs_driver_plugin}

Follow the steps to check the status of your storage driver and plug-in pods and review any error messages.
{: shortdesc}

1. List the pods in the `kube-system` project.

    ```sh
    oc get pods -n kube-system
    ```
    {: pre}

1. If the storage driver and plug-in pods don't show a **Running** status, get more details of the pod to find the root cause. Depending on the status of your pod, the following commands might fail.
    
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
        

1. Check the latest logs for any error messages. [Review the ODF troubleshooting documentation for steps to resolve common errors](/docs/openshift?topic=openshift-sitemap#sitemap_openshift_data_foundation).

## Checking and updating the oc CLI version
{: #debug_storage_ocs_cli}

If you use a `oc` CLI version that does not match at least the major.minor version of your cluster, you might experience unexpected results. For example, [Kubernetes does not support](https://kubernetes.io/releases/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).
{: shortdesc}

1. Verify that the `oc` CLI version that you run on your local machine matches the Kubernetes version that is installed in your cluster. Show the `oc` CLI version that is installed in your cluster and your local machine.
    ```sh
    oc version
    ```
    {: pre}

    Example output:
    ```sh
    Client Version: version.Info{Major:"1", Minor:"23", GitVersion:"v1.33", GitCommit:"641856db18352033a0d96dbc99153fa3b27298e5", GitTreeState:"clean", BuildDate:"2019-03-25T15:53:57Z", GoVersion:"go1.12.1", Compiler:"gc", Platform:"darwin/amd64"}
    Server Version: version.Info{Major:"1", Minor:"23", GitVersion:"v1.33+IKS", GitCommit:"e15454c2216a73b59e9a059fd2def4e6712a7cf0", GitTreeState:"clean", BuildDate:"2019-04-01T10:08:07Z", GoVersion:"go1.11.5", Compiler:"gc", Platform:"linux/amd64"}
    ```   
    {: screen}

    The CLI versions match if you can see the same version in `GitVersion` for the client and the server. You can ignore the `+IKS` part of the version for the server.

2. If the `oc` CLI versions on your local machine and your cluster don't match, either update your cluster or [install a different CLI version on your local machine](/docs/openshift?topic=openshift-cli-install).

## Debugging your ODF resources 
{: #debug_storage_ocs_cluster}

Describe your ODF resources and review the command outputs for any error messages.
{: shortdesc}

1. List the name of your ODF cluster. 
    ```sh
    oc get ocscluster
    ```
    {: pre}

    Example output:
    ```sh
    NAME             AGE
    ocscluster-vpc   71d
    ```
    {: screen}

1. Describe the storage cluster and review the `Events` section of the output for any error messages. 
    ```sh
    oc describe ocscluster <ocscluster-name>
    ```
    {: pre}

1. List the ODF pods in the `kube-system` namespace and verify that they are `Running`.
    ```sh
    oc get pods -n kube-system
    ```
    {: pre}

    Example output
    ```sh
    NAME                                                   READY   STATUS    RESTARTS   AGE
    ibm-keepalived-watcher-5g2gs                           1/1     Running   0          7d21h
    ibm-keepalived-watcher-8l4ld                           1/1     Running   0          7d21h
    ibm-keepalived-watcher-mhkh5                           1/1     Running   0          7d21h
    ibm-master-proxy-static-10.240.128.10                  2/2     Running   0          71d
    ibm-master-proxy-static-10.240.128.11                  2/2     Running   0          71d
    ibm-master-proxy-static-10.240.128.12                  2/2     Running   0          71d
    ibm-ocs-operator-controller-manager-55667f4d68-md4zb   1/1     Running   8          15d
    ibm-vpc-block-csi-controller-0                         4/4     Running   0          48d
    ibm-vpc-block-csi-node-6gnwv                           3/3     Running   0          48d
    ibm-vpc-block-csi-node-j2h62                           3/3     Running   0          48d
    ibm-vpc-block-csi-node-xpwpf                           3/3     Running   0          48d
    vpn-5b8694cdb-pll6z 
    ```
    {: screen}

1. Describe the `ibm-ocs-operator-controller-manager` pod and review the `Events` section in the output for any error messages.
    ```sh
    oc describe pod <ibm-ocs-operator-controller-manager-a1a1a1a> -n kube-system
    ```
    {: pre}

1. Review the logs of the `ibm-ocs-operator-controller-manager`.
    ```sh
    oc logs <ibm-ocs-operator-controller-manager-a1a1a1a> -n kube-system
    ```
    {: pre}

1. Describe NooBaa and review the `Events` section of the output for any error messages.
    ```sh
    oc describe noobaa -n openshift-storage
    ```
    {: pre}

1. Describe the `ibm-storage-metrics-agent` pod and review the `Events` section in the output for any error messages. 
    ```sh
    oc get pods -n kube-system -l name=ibm-storage-metrics-agent
    ```
    {: pre}

    ```sh
    NAME                                                  READY   STATUS    RESTARTS   AGE ibm-storage-metrics-agent-8685869cc6-79qzq   
    ```
    {: screen} 

1. Review the logs from the `ibm-storage-metrics-agent`. 
    ```sh
    oc logs ibm-storage-metrics-agent-xxx -n kube-system
    ```
    {: pre}

1. Describe the `ocscluster` and review the output for error messages.
    ```sh
    oc describe ocscluster <ocscluster-name> -n openshift-storage
    ```
    {: pre}

1. Gather data about the cluster by using the `oc adm must-gather` command.
    ```sh
    oc adm must-gather --image=registry.redhat.io/ocs4/ocs-must-gather-rhel8:latest --dest-dir=ocs_mustgather
    ```
    {: pre}

1. For classic clusters or {{site.data.keyword.satelliteshort}} clusters that use local volumes on the worker node, make sure that the `disk-by-id` for the volumes that you used for the `osd-device-path` and `mon-device-path` parameters exists on the worker nodes. For more information about how to retrieve these volume IDs, see [Gathering your device details](/docs/openshift?topic=openshift-deploy-odf-classic#odf-classic-get-devices)



1. [Review the troubleshooting documentation for steps to solve common errors](/docs/openshift?topic=openshift-sitemap#sitemap_openshift_data_foundation). 
