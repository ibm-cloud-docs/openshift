---

copyright: 
  years: 2014, 2025
lastupdated: "2025-04-28"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, CrashLoopBackOff, pods fail, status, pod, crashing

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Why do pods repeatedly fail to restart or are unexpectedly removed?
{: #ts-app-pod-fail}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}


Your pod was healthy but unexpectedly gets removed or gets stuck in a restart loop. In some cases, the containers will show a `CrashLoopBackOff` status.
{: tsSymptoms}


Your containers might exceed their resource limits, or your pods might be replaced by higher priority pods.  When a Kubernetes container repeatedly fails to start, it enters a `CrashLoopBackOff` state, indicating a persistent restart loop within a pod. This error often occurs due to various issues preventing the container from launching properly. Common causes can include insufficient memory, resource overload, deployment errors, third-party service issues like DNS errors, missing dependencies, or container failures due to port conflicts. 
{: tsCauses}


See the following sections:
{: tsResolve}

* [Fixing container resource limits](#pod-fail-resource-limits)
* [Fixing pod replacement by higher priority pods](#pod-fail-higher-priority)



## Fixing container resource limits
{: #pod-fail-resource-limits}

1. Get the name of your pod. If you used a label, you can include it to filter your results.
    ```sh
    oc get pods --selector='app=wasliberty'
    ```
    {: pre}

2. Describe the pod and look for the **Restart Count**.
    ```sh
    oc describe pod
    ```
    {: pre}

3. If the pod restarted many times in a short period of time, fetch its status.
    ```sh
    oc get pod <pod_name> -n <namespace> -o go-template='{{range.status.containerStatuses}}{{"Container Name: "}}{{.name}}{{"\r\nLastState: "}}{{.lastState}}{{end}}'
    ```
4. Review the reason. For example, `OOM Killed` means out of memory indicating that the container is crashing because of a resource limit.
5. Add capacity to your cluster such as by resizing worker pools so that the resources can be fulfilled. For more information, see [Resize your Classic worker pool](/docs/openshift?topic=openshift-add-workers-classic) or [Resize your VPC worker pool](/docs/openshift?topic=openshift-add-workers-vpc).



## Fixing pod replacement by higher priority pods
{: #pod-fail-higher-priority}

To see if your pod is being replaced by higher priority pods:
1. Get the name of your pod.

    ```sh
    oc get pods
    ```
    {: pre}

2. Describe your pod YAML.

    ```sh
    oc get pod <pod_name> -o yaml
    ```
    {: pre}

3. Check the `priorityClassName` field.

    1. If there is no `priorityClassName` field value, then your pod has the `globalDefault` priority class. If your cluster admin did not set a `globalDefault` priority class, then the default is zero (0), or the lowest priority. Any pod with a higher priority class can preempt, or remove, your pod.

    2. If there is a `priorityClassName` field value, get the priority class.

        ```sh
        oc get priorityclass <priority_class_name> -o yaml
        ```
        {: pre}

    3. Note the `value` field to check your pod's priority.

4. List existing priority classes in the cluster.

    ```sh
    oc get priorityclasses
    ```
    {: pre}

5. For each priority class, get the YAML file and note the `value` field.

    ```sh
    oc get priorityclass <priority_class_name> -o yaml
    ```
    {: pre}

6. Compare your pod's priority class value with the other priority class values to see if it is higher or lower in priority.

7. Repeat steps 1 to 3 for other pods in the cluster, to check what priority class they are using. If those other pods' priority class is higher than your pod, your pod is not provisioned unless there is enough resources for your pod and every pod with higher priority.

8. Contact your cluster admin to add more capacity to your cluster and confirm that the correct priority classes are assigned.
