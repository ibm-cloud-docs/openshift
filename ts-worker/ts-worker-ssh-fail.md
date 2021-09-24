---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-24"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---



{{site.data.keyword.attribute-definition-list}}

# Why can't I SSH into my worker node?
{: #cs_ssh_worker}

**Infrastructure provider**:

- <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
- <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


You cannot access your worker node by using an SSH connection.
{: tsSymptoms}


SSH by password is unavailable on the worker nodes.
{: tsCauses}


To run actions on every worker node, use a Kubernetes [`DaemonSet`](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external}, or use jobs for one-time actions.
{: tsResolve}

To get host access to worker nodes for debugging and troubleshooting purposes, review the following options.

## Debugging by using `oc debug`
{: #oc-debug}

Use the `oc debug node` command to deploy a pod with a privileged `securityContext` to a worker node that you want to troubleshoot.
{: shortdesc}

The debug pod is deployed with an interactive shell so that you can access the worker node immediately after the pod is created. For more information about how the `oc debug node` command works, see [this {{site.data.keyword.redhat_notm}} blog post](https://www.redhat.com/sysadmin/how-oc-debug-works){: external}.

1. Get the name of the worker node that you want to access. The worker node name is its private IP address.
    ```sh
    oc get nodes -o wide
    ```
    {: pre}

2. Create a debug pod that has host access. When the pod is created, the pod's interactive shell is automatically opened. If the `oc debug node` command fails, continue to option 2.
    ```sh
    oc debug node/<NODE_NAME>
    ```
    {: pre}

3. Run debug commands to help you gather information and troubleshoot issues. Commands that you might use to debug, such as `tcpdump`, `curl`, `ip`, `ifconfig`, `nc`, `ping`, and `ps`, are already available in the shell. You can also install other tools, such as `mtr`, by running `yum install <tool>`.



## Debugging by using `kubectl exec`
{: #kubectl-exec}

If you are unable to use the `oc debug node` command, you can create an Alpine pod with a privileged `securityContext` and use the `kubectl exec` command to run debug commands from the pod's interactive shell.
{: shortdesc}

1. Get the name of the worker node that you want to access. The worker node name is its private IP address.

    ```sh
    oc get nodes -o wide
    ```
    {: pre}

2. Export the name in an environment variable.

    ```sh
    export NODE=<NODE_NAME>
    ```
    {: pre}


3. Create a debug pod on the worker node.

    ```yaml
    kubectl apply -f - << EOF
    apiVersion: v1
    kind: Pod
    metadata:
        name: debug-${NODE}
    namespace: default
      spec:
        containers:
        - args: ["-c", "apk add tcpdump mtr curl; sleep 1d"]
          command: ["/bin/sh"]
          image: icr.io/armada-master/alpine:latest
          imagePullPolicy: IfNotPresent
          name: debug
          resources: {}
          securityContext:
            privileged: true
            runAsUser: 0
          volumeMounts:
          - mountPath: /host
            name: host-volume
        volumes:
        - name: host-volume
          hostPath:
            path: /
        dnsPolicy: ClusterFirst
        hostNetwork: true
        hostPID: true
        nodeSelector:
          kubernetes.io/hostname: ${NODE}
        restartPolicy: Never
        securityContext: {}
      EOF
    ```
    {: pre}

4. Log in to the debug pod. The pod's interactive shell is automatically opened. If the `kubectl exec` command fails, continue to option 3.

    ```sh
    kubectl exec -it debug-${NODE} -- sh
    ```
    {: pre}

5. Run debug commands to help you gather information and troubleshoot issues. Commands that you might use to debug, such as `tcpdump`, `mtr`, `curl`, `ip`, `ifconfig`, `nc`, `ping`, and `ps`, are already available in the shell. You can also install other tools, such as `dig`, by running `apk add <tool>`. For example, to add `dig`, run `apk add bind-tools`.

6. Delete the host access pod that you created for debugging.

    ```sh
    kubectl delete pod debug-${NODE}
    ```
    {: pre}



## Debugging by creating a pod with root SSH access
{: #pod-ssh}

If you are unable to use the `oc debug node` or `kubectl exec` commands, such as if the VPN connection between the cluster master and worker nodes is down, you can create a pod that enables root SSH access and copies a public SSH key to the worker node for SSH access.
{: shortdesc}

Allowing root SSH access is a security risk. Only allow SSH access when it is required and no other option is available to troubleshoot worker node issues. When you finish troubleshooting, be sure to follow step 7 in this section to disable SSH access.
{: important}

1. Choose an existing or create a new public SSH key.

2. Get the name of the worker node that you want to access. The worker node name is its private IP address.

    ```sh
    oc get nodes -o wide
    ```
    {: pre}

3. Create the following YAML file for a debug pod, and save the file as `enable-ssh.yaml`. Replace `<NODE_NAME>` with the worker node name and replace the example `value` for `SSH_PUBLIC_KEY` with your public SSH key.

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: enable-ssh-<NODE_NAME>
      namespace: default
    spec:
      tolerations:
      - operator: "Exists"
      hostNetwork: true
      hostPID: true
      hostIPC: true
      containers:
      - image: icr.io/armada-master/alpine:latest
        env:
        - name: SSH_PUBLIC_KEY
          value: "<ssh-rsa AAA...ZZZ user@ibm.com>"
        args: ["-c", "echo $(SSH_PUBLIC_KEY) | tee -a /root/.ssh/authorized_keys && sed -i 's/PermitRootLogin.*/PermitRootLogin yes/g' /host/etc/ssh/sshd_config && killall -1 sshd && while true; do sleep 86400; done"]
        command: ["/bin/sh"]
        name: enable-ssh
        securityContext:
          privileged: true
        volumeMounts:
        - mountPath: /host
          name: host-volume
        - mountPath: /root/.ssh
          name: ssh-volume
      volumes:
      - name: host-volume
        hostPath:
          path: /
      - name: ssh-volume
        hostPath:
          path: /root/.ssh
      nodeSelector:
        kubernetes.io/hostname: <NODE_NAME>
      restartPolicy: Never
    ```
    {: codeblock}

4. Create the pod in your cluster. When this pod is created, your public key is added to the worker node and SSH is configured to allow root SSH login.

    ```sh
    oc apply -f enable-ssh.yaml
    ```
    {: pre}

5. Use the private or public network to access the worker node by using your SSH key.

### Private network
{: #ssh-private-network}

Create a new or choose an existing server instance that has access to the same private network as the worker node. For VPC clusters, the [virtual server instance](https://cloud.ibm.com/vpc-ext/compute/vs){: external} must exist in the same VPC as the worker node.
{: shortdesc}

For classic clusters, the [device](https://cloud.ibm.com/gen1/infrastructure/devices){: external} can access the worker node from any private VLAN if a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) or [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning) is enabled. Otherwise, the device must exist on the same private VLAN as the worker node.

1. Copy your SSH private key from step 1 from your local machine to this server instance.

    ```sh
    scp <SSH_private_key_location> <user@host>:/.ssh/id_rsa_worker_private
    ```
    {: pre}

2. SSH into the server instance.
    
3. Set the correct permissions for using the SSH private key that you copied.
    
    ```sh
    chmod 400 ~/.ssh/id_rsa_worker_private
    ```
    {: pre}

4. Use the private key to SSH into the worker node that you found in step 2.

    ```sh
    ssh -i ~/.ssh/id_rsa_worker_private root@<WORKER_PRIVATE_IP>
    ```
    {: pre}

### Public network classic clusters that are connected to a public VLAN only
{: #public-network-only-classic-debug}

Debug classic clusters that are connected to a public VLAN by logging in to your worker nodes.
{: shortdesc}
        
1. [Install and configure the Calico CLI, and set the context for your cluster to run Calico commands](/docs/openshift?topic=openshift-network_policies#cli_install).

2. Create a Calico global network policy that is named `ssh-open` to allow inbound SSH traffic on port 22.

    ```sh
    calicoctl apply [-c <path_to_calicoctl_cfg>/calicoctl.cfg] -f - <<EOF
    apiVersion: projectcalico.org/v3
    kind: GlobalNetworkPolicy
    metadata:
      name: ssh-open
    spec:
      selector: ibm.role == 'worker_public'
      ingress:
      - action: Allow
        protocol: TCP
        destination:
          ports:
          - 22
      - action: Allow
        protocol: UDP
        destination:
          ports:
          - 22
      order: 1500
    EOF
    ```
    {: pre}

3. Get the public IP address of your worker node.

    ```sh
    oc get nodes -o wide
    ```
    {: pre}

4. Use the SSH private key from step 1 to SSH into the worker node via its public IP address.

    ```sh
    ssh -i ~/.ssh/id_rsa_worker_private root@<WORKER_PUBLIC_IP>
    ```
    {: pre}

6. Run debug commands to help you gather information and troubleshoot issues, such as `ip`, `ifconfig`, `nc`, `tcpdump`, `ping`, `ps`, and `curl`. You can also install other tools, such as `mtr`, by running `yum install <tool>`.

### Cleaning up after debugging
{: #ssh-debug-cleanup}

After you finish debugging, clean up resources to disable SSH access.
{: shortdesc}

1. Delete the SSH enablement pod.

    ```sh
    oc delete pod enable-ssh-<NODE_NAME>
    ```
    {: pre}

2. If you accessed the worker node via the public network, delete the Calico policy so that port 22 is blocked again.
    ```sh
    calicoctl delete gnp ssh-open [-c <path_to_calicoctl_cfg>/calicoctl.cfg]
    ```
    {: pre}

3. [Reload your classic worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) or [replace your VPC worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) so that the original SSH configuration is used and the SSH key that you added is removed.





