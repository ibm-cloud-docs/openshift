---

copyright: 
  years: 2023
lastupdated: "2023-10-30"

keywords: flow logs, VPC monitoring, worker nodes, VPC, network traffic, collector, LinuxONE worker nodes, s390x architecture, fluentd, log Analysis

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Configuring the Fluentd and {{site.data.keyword.la_short}} service for LinuxONE worker nodes
{: #s390x-fluentd-log}

[Virtual Private Cloud]{: tag-vpc}

You can configure a logging agent by using Fluentd in your cluster, and then the Fluentd based agent collects logs from the paths in the LinuxONE worker nodes. Fluentd can then forward these logs to your {{site.data.keyword.la_full_notm}} service instance, so that you can view logs of the cluster with LinuxONE worker nodes.
{: shortdesc}

To configure the Fluentd based agent with your {{site.data.keyword.la_full_notm}} instance, complete the following steps. 

1. Create an [{{site.data.keyword.la_full_notm}} service instance](/docs/log-analysis?topic=log-analysis-getting-started) and note the name of the instance. The service instance must belong to the same {{site.data.keyword.cloud_notm}} account where you created your cluster, but can be in a different resource group and {{site.data.keyword.cloud_notm}} region than your cluster.

2. Create a logging specific namespace such as `ibm-observe` on your cluster by using the following command.
    
    ```sh
    kubectl create namespace ibm-observe
    ```
    {: pre}

3. Get the [ingestion key](/docs/log-analysis?topic=log-analysis-ingestion_key) and the region specific URL of your {{site.data.keyword.la_full_notm}} instance. For example, `<ingestion-key>` and `<region-specific-log-instance-url>`.

4. Copy the following example code into a new file such as `fluentd-cm.yaml`, and replace the `<ingestion-key>` and `<region-specific-log-instance-url>` in the yaml file with the values from the previous step.
    
    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: fluentd-config
      namespace: ibm-observe
      labels:
           app: fluentd-agent
           kubernetes.io/cluster-service: "true"
    data:
     fluent.conf: |
       <source>
           @type tail
           path /var/data/kubeletlogs/**/**/*.log
           exclude_path ["/var/data/kubeletlogs/*fluentd*/fluentd/*.log"]
           tag "**"
           format none
           read_from_head true
       </source>
   
       <match **>
           @type http
           endpoint https://<region-specific-log-instance-url>/logs/ingest?hostname=fluentd-agent
           open_timeout 2
           json_array false
           content_type text/plain
           headers {"apikey":"<ingestion-key>"}
           error_response_as_unrecoverable false
           <format>
               @type json
           </format>
           <buffer>
               flush_interval 10s
           </buffer>
       </match>
    ```
    {: codeblock}
    
    
5. Apply the configuration in the yaml file to the cluster.

    ```sh
    kubectl apply -f fluentd-cm.yaml
    ```
    {: pre}
   
6. Create another yaml file such as `fluentd.yaml` with the following code example. Note the `namespace` value must be the same as the logging specific name space created in the previous step.
    
    ```yaml
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: fluentd
      namespace: ibm-observe
   
    ---
   
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRole
    metadata:
      name: fluentd
    rules:
    - apiGroups:
      - ""
      resources:
      - pods
      - namespaces
      verbs:
      - get
      - list
      - watch
   
    ---
   
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      name: fluentd
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: fluentd
    subjects:
    - kind: ServiceAccount
      name: fluentd
      namespace: ibm-observe
   
   ---
   
   apiVersion: apps/v1
   kind: DaemonSet
   metadata:
     name: fluentd
     namespace: ibm-observe
   spec:
     selector:
       matchLabels:
         app: fluentd
     template:
       metadata:
         labels:
           app: fluentd 
       spec:
         serviceAccountName: fluentd
         containers:
           - name: fluentd
             image: fluentd:latest
             env:
              - name: FLUENT_UID
                value: "0" 
             securityContext:
               runAsUser: 1000
             volumeMounts:
             - name: varlog
               mountPath: /var/log
             - name: varlibdockercontainers
               mountPath: /var/lib/docker/containers
               readOnly: true
             - name: vardata
               mountPath: /var/data
             - name: mnt
               mountPath: /mnt
               readOnly: true
             - name: docker
               mountPath: /var/run/docker.sock
             - name: osrelease
               mountPath: /etc/os-release
             - name: fluenthostname
               mountPath: /etc/fluenthostname
             - name: fluentd-config
               mountPath: /fluentd/etc 
             env:
               - name: TAG
                 value: "**"
         volumes:
         - name: varlog
           hostPath:
             path: /var/log
         - name: varlibdockercontainers
           hostPath:
             path: /var/lib/docker/containers
         - name: vardata
           hostPath:
             path: /var/data
         - name: mnt
           hostPath:
             path: /mnt
         - name: docker
           hostPath:
             path: /var/run/docker.sock
         - name: osrelease
           hostPath:
             path: /etc/os-release
         - name: fluenthostname
           hostPath:
             path: /etc/hostname
         - name: fluentd-config
           configMap:
             name: fluentd-config
   ```
   {: codeblock}
   
   
7. Apply the configuration in the yaml file to the cluster.
    
    ```sh
    kubectl apply -f fluentd.yaml
    ```
    {: pre}
   
8. View [the logs on the {{site.data.keyword.la_short}} dashboard](/docs/log-analysis?topic=log-analysis-kube#kube_step3).



