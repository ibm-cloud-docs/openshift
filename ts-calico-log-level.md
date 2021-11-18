---

copyright: 
  years: 2021, 2021
lastupdated: "2021-11-18"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Debugging Calico components
{: #calico_log_level}
{: troubleshoot}
{: support}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

These instructions apply to {{site.data.keyword.openshiftlong}} 3.11.
{: note}


You experience issues with Calico components such as pods that don't deploy or intermittent networking issues. 
{: tsSymptoms}


Increase the logging level of Calico components to gather more information about the issue.
{: tsResolve}

## Increasing the log level for components.
{: #calico-increase-logging}

Complete the following steps to increase the log level for the `calico-typha` component.

1. Run the following command to edit the `calico-typha` deployment. 

    ```sh
    oc edit deploy -n kube-system calico-typha
    ```
    {: pre}


    
2. Change the `TYPHA_LOGSEVERITYSCREEN` environment variable from `info` to `debug`.
  ```sh
        containers:
      - env:
        - name: TYPHA_LOGSEVERITYSCREEN
          value: debug
  ```
  {: screen}

    
3. Save and close the file to apply the changes and restart the `calico-typha` deployment.

Complete the following steps to increase the log level for the `calico-cni` component.

1. Run the following command to edit the `calico-config` configmap.  
    
    ```sh
    oc edit cm -n kube-system calico-config
    ```
    {: pre}
    
2. Change the `cni_network_config` > `plugins` > `log_level` environment variable to `debug`.
  ```sh
    cni_network_config: |-
    {
      "name": "k8s-pod-network",
      "cniVersion": "0.3.1",
      "plugins": [
        {
          "type": "calico",
          "log_level": "debug",
  ```
  {: screen}
  
3. Save and close the file. The change won't take effect until the `calico-node` pods are restarted. 

4. Restart the `calico-node` pods to apply the changes.
    
      ```sh
      oc rollout restart daemonset/calico-node -n kube-system
      ```
      {: pre}

      
      Example output
      ```sh
      daemonset.apps/calico-node restarted
      ```
      {: screen}
      
Complete the following steps to increase the log level for the `calico-node` component.

1. Run the following command: 
    
    ```sh
    oc edit ds -n kube-system calico-node
    ```
    {: pre}
    

2. Under the `FELIX_USAGEREPORTINGENABLED` name and value pair (or after any of the `FELIX_*` environment variable name value pairs), add the following entry:
    ```sh
    - name: FELIX_LOGSEVERITYSCREEN
      value: Debug
    ```
    {: pre}    
    
3. Save the change. After saving your changes, all the pods in the `calico-node` daemonset complete a rolling update which applies the changes. The `calico-cni` also applies any changes to logging levels in the `kube-system/calico-config` configmap.

Complete the following steps to increase the log level for the `calico-kube-controllers` component.

1. Edit the daemonset by running the following command. 
    
    ```sh
    oc edit ds -n kube-system calico-node
    ```
    {: pre}
    
    
2. Under the `DATASTORE_TYPE` name and value pair, add the following entry:
    ```sh
    - name: LOG_LEVEL
      value: debug
    ```
    {: pre}
3. Save the change. The `calico-kube-controllers` pod restarts and applies the changes.


## Gathering Calico logs
{: #calico-log-gather}

1. List the pods and nodes in your cluster and make a node of the pod name, pod IP address, and worker note where the issue occured.
2. Get the logs for the `calico-node` pod on the worker node where the problem occurred.
  ```sh
  oc logs calico-typha-aaa11111a-aaaaa -n kube-system
  ```
  {: pre}

3. Get logs for the `calico-kube-controllers` pod.
  ```sh
  oc logs calico-kube-controllers-11aaa11aa1-a1a1a -n kube-system
  ```
  {:  pre}
  
4. Follow the instructions for [Debugging by using oc exec](/docs/openshift?topic=openshift-cs_ssh_worker#kubectl-exec) to get `/var/log/syslog`, `containerd.log`, `kubelet.log`, and `kern.log` from the worker node.


