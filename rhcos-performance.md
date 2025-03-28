---

copyright: 
  years: 2022, 2025
lastupdated: "2025-03-28"


keywords: openshift, kernel, rhcos, cpu pinning, huge pages, numa, core os

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Tuning performance for Red Hat CoreOS worker nodes
{: #rhcos-performance}

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}

Supported worker node operating systems
:   Red Hat CoreOS (`RHCOS`)

You can tune your Red Hat CoreOS worker node performance by enabling CPU Pinning, non-uniform memory access (NUMA), and huge pages configurations. These configurations can be beneficial for applications that have strict performance requirements. However, these customizations might cause issues with scheduling workloads.
{: shortdesc}

Instead of tuning worker node performance with `MachineConfig` files in {{site.data.keyword.redhat_openshift_notm}}, you can modify the host with a `daemonset` file. For more information, see [Changing the Calico MTU](/docs/openshift?topic=openshift-kernel#calico-mtu) or [Tuning performance for Red Hat CoreOS worker nodes](/docs/openshift?topic=openshift-rhcos-performance).
{: note} 


## Deploying the Node Feature Discovery Operator
{: #rhcos-node-feature-discovery}

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}

Before you can enable NUMA, CPU pinning, and huge pages on your worker nodes, you must deploy the Node Feature Discovery Operator. For more information, see [The Node Feature Discovery Operator](https://docs.redhat.com/documentation/openshift_container_platform/4.8/html/scalability_and_performance/node-feature-discovery-operator){: external}.

## Enabling non-uniform memory access (NUMA), CPU pinning, and huge pages on your worker nodes
{: #rhcos-numa-pinning-huge}

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}

Before you begin, make sure that you have deployed the [Node Feature Discovery Operator](#rhcos-node-feature-discovery).

1. Save the following `DaemonSet` to a file called `customize.yaml`

    ```yaml
    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      name: ibm-user-custom-configurator-privileged
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: system:openshift:scc:privileged
    subjects:
      - kind: ServiceAccount
        name: ibm-user-custom-configurator
        namespace: kube-system
    ---
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: ibm-user-custom-configurator
      namespace: kube-system
    ---
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: ibm-user-custom-configurator
      namespace: kube-system
    data:
      89-hugepages.conf: |
        vm.nr_hugepages=<<NUMBER_OF_HUGEPAGES>>
      configure.sh: |
        #!/usr/bin/env bash
        set -x
        cp -f /scripts/ibm-user-custom-configuration.sh /host-usr-local-bin/ibm-user-custom-configuration.sh
        chmod 0755 /host-usr-local-bin/ibm-user-custom-configuration.sh
        cp -f /scripts/ibm-user-custom-configuration.service /host-etc-systemd-dir/ibm-user-custom-configuration.service
        chmod 0644 /host-etc-systemd-dir/ibm-user-custom-configuration.service
        if [[ -f /scripts/89-hugepages.conf ]]; then
          cp -f /scripts/89-hugepages.conf /host-etc-systctld-dir/89-hugepages.conf
        fi
        nsenter -t 1 -m -u -i -n -p -- systemctl daemon-reload
        nsenter -t 1 -m -u -i -n -p -- systemctl enable ibm-user-custom-configuration.service
        nsenter -t 1 -m -u -i -n -p -- systemctl start ibm-user-custom-configuration.service
      ibm-user-custom-configuration.sh: |
        #!/usr/bin/env bash
        set -x
        GIGABYTES_RESERVED_MEMORY=$(echo $SYSTEM_RESERVED_MEMORY | awk -F 'Gi' '{print $1}')
        GIGABYTES_RESERVED_MEMORY_ROUNDED_UP=$(echo $GIGABYTES_RESERVED_MEMORY | awk '{print int($1+0.999)}')
        sed -i "s/SYSTEM_RESERVED_MEMORY=.*/SYSTEM_RESERVED_MEMORY=${GIGABYTES_RESERVED_MEMORY_ROUNDED_UP}Gi/g" /etc/node-sizing.env
        TOTAL_NUMA_MEMORY_TO_ALLOCATE=$(echo "$GIGABYTES_RESERVED_MEMORY_ROUNDED_UP" "1024" | awk '{print $1 * $2 + 100}')
        if cat /etc/kubernetes/kubelet.conf | jq -r .; then
          cat >/tmp/ibm-user-config.conf.json <<EOF
          {
            "topologyManagerPolicy": "<<TOPOLOGY_MANAGER_POLICY_VALUE>>",
            "memoryManagerPolicy": "Static",
            "cpuManagerPolicy": "static",
            "reservedMemory": [
              {
                "numaNode": 0,
                "limits": {
                "memory": "${TOTAL_NUMA_MEMORY_TO_ALLOCATE}Mi"
                  }
              }
            ]
          }
        EOF
          if ! cat /tmp/ibm-user-config.conf.json | jq -r .; then
            exit 1
          fi
          if ! jq -s '.[0] * .[1]' /tmp/ibm-user-config.conf.json /etc/kubernetes/kubelet.conf > /etc/kubernetes/tmp-kubelet.conf; then
            exit 1
          fi
          mv -f /etc/kubernetes/tmp-kubelet.conf /etc/kubernetes/kubelet.conf
          else
            cat >/tmp/ibm-user-config.conf <<EOF
        #START USER CONFIG
        topologyManagerPolicy: <<TOPOLOGY_MANAGER_POLICY_VALUE>>
        memoryManagerPolicy: Static
        cpuManagerPolicy: static
        reservedMemory:
          - numaNode: 0
            limits:
              memory: ${TOTAL_NUMA_MEMORY_TO_ALLOCATE}Mi
        #END USER CONFIG
        EOF
          sed -i '/#START USER CONFIG/,/#END USER CONFIG/d' /etc/kubernetes/kubelet.conf
          cat /tmp/ibm-user-config.conf >>/etc/kubernetes/kubelet.conf
        fi
      ibm-user-custom-configuration.service: |
        [Unit]
        Description=Add custom user config to kubelet
        Before=kubelet.service
        After=kubelet-auto-node-size.service
        
        [Service]
        Type=oneshot
        RemainAfterExit=yes
        EnvironmentFile=/etc/node-sizing.env
        ExecStart=/usr/local/bin/ibm-user-custom-configuration.sh
        
        [Install]
        WantedBy=multi-user.target
    ---
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      labels:
        app: ibm-user-custom-configurator
      name: ibm-user-custom-configurator
      namespace: kube-system
    spec:
      selector:
        matchLabels:
          app: ibm-user-custom-configurator
      template:
        metadata:
          labels:
            app: ibm-user-custom-configurator
        spec:
          nodeSelector:
            feature.node.kubernetes.io/memory-numa: "true"
            ibm-cloud.kubernetes.io/os: RHCOS
          tolerations:
            - operator: "Exists"
          hostPID: true
          serviceAccount: ibm-user-custom-configurator
          initContainers:
            - name: configure
              image: "registry.access.redhat.com/ubi8/ubi:8.6"
              command: ['/bin/bash', '-c', 'mkdir /cache && cp /scripts/configure.sh /cache && chmod +x /cache/configure.sh && /bin/bash /cache/configure.sh']
              securityContext:
                privileged: true
              volumeMounts:
                - mountPath: /scripts
                  name: script-config
                - mountPath: /host-etc-systemd-dir
                  name: etc-systemd-dir
                - mountPath: /host-usr-local-bin
                  name: usr-local-bin
                - mountPath: /host-etc-systctld-dir
                  name: etc-systctld-dir
          containers:
            - name: pause
              image: registry.ng.bluemix.net/armada-master/pause:3.2
          volumes:
            - name: etc-systemd-dir
              hostPath:
                path: /etc/systemd/system
            - name: etc-systctld-dir
              hostPath:
                path: /etc/sysctl.d
            - name: usr-local-bin
              hostPath:
                path: /usr/local/bin
            - name: script-config
              configMap:
                name: ibm-user-custom-configurator
    ```
    {: codeblock}
    
    
1. Edit the `DaemonSet` values to tune performance.

    `NUMBER_OF_HUGEPAGES`
    :   Enter the number of huge pages that you want to allocate. For example: `2048`. If you don't want to enable huge pages, enter `0`. The more huge pages you allocate, the less overall memory is available to your applications.
    
    `TOPOLOGY_MANAGER_POLICY_VALUE`
    :   Enter the topology manager policies that you want to use. The `best-effort` topology is recommended to ensure maximum scheduling availability. However, you can use other topologies for more strict requirements validation while reducing workload scheduling availability. For more information, see [Topology manager](https://kubernetes.io/docs/tasks/administer-cluster/topology-manager/){: external}. 
    
    You can edit the `nodeSelector` section to only apply the configuration to a subset of your worker nodes.
    {: tip}
    
1. Apply the `DaemonSet` by running the following command.
    ```sh
    kubectl replace --force -f customize.yaml
    ```
    {: pre}
    
1. Verify that the pods have entered the `Running` state.
    ```sh
    kubectl get pods -n kube-system -l app=ibm-user-custom-configurator -o wide
    ```
    {: pre}
    
1. After the pods are running, reboot each worker node.
    1. Deploy a debug pod on your worker node.
        ```sh
        oc debug node/NODE_NAME
        ```
        {: pre}
    
    1. After the debug session starts, run the following command.
        ```sh
        nsenter -t 1 -m -u -i -n -p -- reboot
        ```
        {: pre}
        
    1. Repeat these steps for each worker node that you want to reboot.
    
    
## Enabling CPU pinning and huge pages on your worker nodes
{: #rhcos-pinning-huge}

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}

Before you begin, make sure that you have deployed the [Node Feature Discovery Operator](#rhcos-node-feature-discovery).

1. Save the following `DaemonSet` to a file called `cpu-pinning.yaml`.

    ```yaml
    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      name: ibm-user-custom-configurator-privileged
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: system:openshift:scc:privileged
    subjects:
      - kind: ServiceAccount
        name: ibm-user-custom-configurator
        namespace: kube-system
    ---
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: ibm-user-custom-configurator
      namespace: kube-system
    ---
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: ibm-user-custom-configurator
      namespace: kube-system
    data:
      89-hugepages.conf: |
        vm.nr_hugepages=<<NUMBER_OF_HUGEPAGES>>
      configure.sh: |
        #!/usr/bin/env bash
        set -x
        cp -f /scripts/ibm-user-custom-configuration.sh /host-usr-local-bin/ibm-user-custom-configuration.sh
        chmod 0755 /host-usr-local-bin/ibm-user-custom-configuration.sh
        cp -f /scripts/ibm-user-custom-configuration.service /host-etc-systemd-dir/ibm-user-custom-configuration.service
        chmod 0644 /host-etc-systemd-dir/ibm-user-custom-configuration.service
        if [[ -f /scripts/89-hugepages.conf ]]; then
          cp -f /scripts/89-hugepages.conf /host-etc-systctld-dir/89-hugepages.conf
        fi
        nsenter -t 1 -m -u -i -n -p -- systemctl daemon-reload
        nsenter -t 1 -m -u -i -n -p -- systemctl enable ibm-user-custom-configuration.service
        nsenter -t 1 -m -u -i -n -p -- systemctl start ibm-user-custom-configuration.service
      ibm-user-custom-configuration.sh: |
        #!/usr/bin/env bash
        set -x
        if cat /etc/kubernetes/kubelet.conf | jq -r .; then
          cat >/tmp/ibm-user-config.conf.json <<EOF
          {
            "cpuManagerPolicy": "static"
          }
        EOF
          if ! cat /tmp/ibm-user-config.conf.json | jq -r .; then
            exit 1
          fi
          if ! jq -s '.[0] * .[1]' /tmp/ibm-user-config.conf.json /etc/kubernetes/kubelet.conf > /etc/kubernetes/tmp-kubelet.conf; then
            exit 1
          fi
          mv -f /etc/kubernetes/tmp-kubelet.conf /etc/kubernetes/kubelet.conf
        else
          cat >/tmp/ibm-user-config.conf <<EOF
        #START USER CONFIG
        cpuManagerPolicy: static
        #END USER CONFIG
        EOF
          sed -i '/#START USER CONFIG/,/#END USER CONFIG/d' /etc/kubernetes/kubelet.conf
          cat /tmp/ibm-user-config.conf >>/etc/kubernetes/kubelet.conf
        fi
      ibm-user-custom-configuration.service: |
        [Unit]
        Description=Add custom user config to kubelet
        Before=kubelet.service
        After=kubelet-auto-node-size.service
        
        [Service]
        Type=oneshot
        RemainAfterExit=yes
        EnvironmentFile=/etc/node-sizing.env
        ExecStart=/usr/local/bin/ibm-user-custom-configuration.sh    
        [Install]
        WantedBy=multi-user.target
    ---
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      labels:
        app: ibm-user-custom-configurator
      name: ibm-user-custom-configurator
      namespace: kube-system
    spec:
      selector:
        matchLabels:
          app: ibm-user-custom-configurator
      template:
        metadata:
          labels:
            app: ibm-user-custom-configurator
        spec:
          nodeSelector:
            ibm-cloud.kubernetes.io/os: RHCOS
          tolerations:
            - operator: "Exists"
          hostPID: true
          serviceAccount: ibm-user-custom-configurator
          initContainers:
            - name: configure
              image: "registry.access.redhat.com/ubi8/ubi:8.6"
              command: ['/bin/bash', '-c', 'mkdir /cache && cp /scripts/configure.sh /cache && chmod +x /cache/configure.sh && /bin/bash /cache/configure.sh']
              securityContext:
                privileged: true
              volumeMounts:
                - mountPath: /scripts
                  name: script-config
                - mountPath: /host-etc-systemd-dir
                  name: etc-systemd-dir
                - mountPath: /host-usr-local-bin
                  name: usr-local-bin
                - mountPath: /host-etc-systctld-dir
                  name: etc-systctld-dir
          containers:
            - name: pause
              image: registry.ng.bluemix.net/armada-master/pause:3.2
          volumes:
            - name: etc-systemd-dir
              hostPath:
                path: /etc/systemd/system
            - name: etc-systctld-dir
              hostPath:
                path: /etc/sysctl.d
            - name: usr-local-bin
              hostPath:
                path: /usr/local/bin
            - name: script-config
              configMap:
                name: ibm-user-custom-configurator
    ```
    {: codeblock}

1. Edit the `DaemonSet` values to tune performance.

    `NUMBER_OF_HUGEPAGES`
    :   Enter the number of huge pages that you want to allocate. For example: `2048`. If you don't want to enable huge pages, enter `0`. The more huge pages you allocate, the less overall memory is available to your applications.
    
    You can edit the `nodeSelector` section to only apply the configuration to a subset of your worker nodes.
    {: tip}
    
1. Apply the `DaemonSet` by running the following command.
    ```sh
    kubectl replace --force -f cpu-pinnning.yaml
    ```
    {: pre}
    
1. Verify that the pods have entered the `Running` state.
    ```sh
    kubectl get pods -n kube-system -l app=ibm-user-custom-configurator -o wide
    ```
    {: pre}
    
1. After the pods are running, reboot each worker node.
    1. Deploy a debug pod on your worker node.
        ```sh
        oc debug node/NODE_NAME
        ```
        {: pre}
    
    1. After the debug session starts, run the following command.
        ```sh
        nsenter -t 1 -m -u -i -n -p -- reboot
        ```
        {: pre}
        
    1. Repeat these steps for each worker node that you want to reboot.

## Enabling `kernel-devel` packages
{: #enable-kernel-devel}

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}

You might need to enable `kernel-devel` packages to use {{site.data.keyword.satelliteshort}} services or storage such as Spectrum Scale Fusion.

Complete the following steps to enable `kernel-devel` by applying a custom config map and machine config to your worker nodes.

1. Run the following command to apply the `MachineConfig`.

    ```sh
    ibmcloud ks cluster config --cluster CLUSTERID 
    cat >"/tmp/kernel-devel-payload.yaml" <<EOF
    apiVersion: v1
    kind: List
    metadata:
      name: pvg-machine-config-tester
      annotations:
    items:
      - apiVersion: v1
        kind: Namespace
        metadata:
          name: ibm-machine-config
      - apiVersion: v1
        data:
          config: |+
            apiVersion: machineconfiguration.openshift.io/v1
            kind: MachineConfig
            metadata:
              name: 97-kerneldevel
              labels:
                machineconfiguration.openshift.io/role: worker
            spec:
              config:
                ignition:
                  version: 3.2.0
              extensions:
              - kernel-devel
        kind: ConfigMap
        metadata:
          labels:
            ibm-cloud.kubernetes.io/user-specified-config: "true"
          name: user-ignition-config-97-kerneldevel
          namespace: ibm-machine-config
    EOF
    kubectl apply -f /tmp/kernel-devel-payload.yaml
    ```
    {: codeblock}

1. Wait for the resources to deploy. This might take 5 minutes or more.

1. Review the details of the config map to confirm that deployment was successful.

    1. Confirm that the `config-validation="valid"` field is present.

        ```sh
        kubectl get cm -n ibm-machine-config user-ignition-config-97-kerneldevel -o yaml | grep config-validation
        ```
        {: pre}

    1. Confirm that `user-ignition-config-97-kerneldevel` is present in the config map.
        ```sh
        kubectl get cm -n ibm-machine-config -l ibm-cloud.kubernetes.io/nodepoolfeedback="true" -o yaml | grep user-ignition-config-97-kerneldevel
        ```
        {: pre}

1. Add worker nodes to your cluster. Worker nodes that you add have `kernel-devel` enabled.

1. Verify `kernel-devel` is enabled.
    1. Start a debug pod on one of your nodes.
        ```sh
        oc debug node/NODEIP
        ```
        {: pre}

    1. Run the following `nsenter` command.
        ```sh
        nsenter -t 1 -m -u -i -n -p -- rpm -qa | grep kernel-devel
        ```
        {: pre}

1. **Optional**: If you no longer need `kernel-devel`, you can remove it by running the following command.
    ```sh
    kubectl delete cm -n ibm-machine-config user-ignition-config-97-kerneldevel
    ```
    {: pre}

## Removing performance customizations
{: #rhcos-performance-remove}

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}

If you want to remove customizations from your worker nodes and reset them to the default configurations, apply the following `DaemonSet`.

1. Save the following `DaemonSet` to a file called `remove-custom.yaml`.

    ```yaml
    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
      name: ibm-user-custom-configurator-privileged
    roleRef:
      apiGroup: rbac.authorization.k8s.io
      kind: ClusterRole
      name: system:openshift:scc:privileged
    subjects:
      - kind: ServiceAccount
        name: ibm-user-custom-configurator
        namespace: kube-system
    ---
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: ibm-user-custom-configurator
      namespace: kube-system
    ---
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: ibm-user-custom-configurator
      namespace: kube-system
    data:
      89-hugepages.conf: |
        vm.nr_hugepages=0
      configure.sh: |
        #!/usr/bin/env bash
        set -x
        cp -f /scripts/ibm-user-custom-configuration.sh /host-usr-local-bin/ibm-user-custom-configuration.sh
        chmod 0755 /host-usr-local-bin/ibm-user-custom-configuration.sh
        cp -f /scripts/ibm-user-custom-configuration.service /host-etc-systemd-dir/ibm-user-custom-configuration.service
        chmod 0644 /host-etc-systemd-dir/ibm-user-custom-configuration.service
        if [[ -f /scripts/89-hugepages.conf ]]; then
          cp -f /scripts/89-hugepages.conf /host-etc-systctld-dir/89-hugepages.conf
        fi
        nsenter -t 1 -m -u -i -n -p -- systemctl daemon-reload
        nsenter -t 1 -m -u -i -n -p -- systemctl enable ibm-user-custom-configuration.service
        nsenter -t 1 -m -u -i -n -p -- systemctl start ibm-user-custom-configuration.service
      ibm-user-custom-configuration.sh: |
        #!/usr/bin/env bash
        set -x
        if cat /etc/kubernetes/kubelet.conf | jq -r .; then
          if ! jq 'del(.topologyManagerPolicy, .memoryManagerPolicy, .cpuManagerPolicy, .reservedMemory)' /etc/kubernetes/kubelet.conf > /etc/kubernetes/tmp-kubelet.conf; then
            exit 1
          fi
          mv -f /etc/kubernetes/tmp-kubelet.conf /etc/kubernetes/kubelet.conf
        else
          sed -i '/#START USER CONFIG/,/#END USER CONFIG/d' /etc/kubernetes/kubelet.conf
        fi
      ibm-user-custom-configuration.service: |
        [Unit]
        Description=Add custom user config to kubelet
        Before=kubelet.service
        After=kubelet-auto-node-size.service
        
        [Service]
        Type=oneshot
        RemainAfterExit=yes
        EnvironmentFile=/etc/node-sizing.env
        ExecStart=/usr/local/bin/ibm-user-custom-configuration.sh
        
        [Install]
        WantedBy=multi-user.target
    ---
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      labels:
        app: ibm-user-custom-configurator
      name: ibm-user-custom-configurator
      namespace: kube-system
    spec:
      selector:
        matchLabels:
          app: ibm-user-custom-configurator
      template:
        metadata:
          labels:
            app: ibm-user-custom-configurator
        spec:
          nodeSelector:
            ibm-cloud.kubernetes.io/os: RHCOS
          tolerations:
            - operator: "Exists"
          hostPID: true
          serviceAccount: ibm-user-custom-configurator
          initContainers:
            - name: configure
              image: "registry.access.redhat.com/ubi8/ubi:8.6"
              command: ['/bin/bash', '-c', 'mkdir /cache && cp /scripts/configure.sh /cache && chmod +x /cache/configure.sh && /bin/bash /cache/configure.sh']
              securityContext:
                privileged: true
              volumeMounts:
                - mountPath: /scripts
                  name: script-config
                - mountPath: /host-etc-systemd-dir
                  name: etc-systemd-dir
                - mountPath: /host-usr-local-bin
                  name: usr-local-bin
                - mountPath: /host-etc-systctld-dir
                  name: etc-systctld-dir
          containers:
            - name: pause
              image: registry.ng.bluemix.net/armada-master/pause:3.2
          volumes:
            - name: etc-systemd-dir
              hostPath:
                path: /etc/systemd/system
            - name: etc-systctld-dir
              hostPath:
                path: /etc/sysctl.d
            - name: usr-local-bin
              hostPath:
                path: /usr/local/bin
            - name: script-config
              configMap:
                name: ibm-user-custom-configurator
    ```
    {: codeblock}
    
1. Apply the `DaemonSet` to your cluster by running the following command.

    ```sh
    kubectl replace --force -f remove-custom.yaml
    ```
    {: pre}

1. Check that the pods have entered the `Running` state.
    ```sh
    kubectl get pods -n kube-system -l app=ibm-user-custom-configurator -o wide
    ```
    {: pre} 
    
1. After the pods are running, reboot each worker node.
    1. Deploy a debug pod on your worker node.
        ```sh
        oc debug node/NODE_NAME
        ```
        {: pre}
    
    1. After the debug session starts, run the following command.
        ```sh
        nsenter -t 1 -m -u -i -n -p -- reboot
        ```
        {: pre}
        
    1. Repeat these steps for each worker node that you want to reboot.
