---

copyright: 
  years: 2014, 2026
lastupdated: "2026-01-06"


keywords: openshift, kubernetes, logmet, logs, metrics, audit, events

subcollection: openshift


---


{{site.data.keyword.attribute-definition-list}}





# Reviewing service, API server, and worker node logs
{: #health-audit}

With audit logs, you're able to understand better what operations are initiated by users in your cluster, which can help you troubleshoot issues or report compliance to industry and internal standards.
{: shortdesc}

## Kubernetes API server audit logs
{: #audit-api-server}

To monitor user-initiated, Kubernetes administrative activity made within your cluster, you can collect and forward audit events that are passed through your Kubernetes API server to {{site.data.keyword.logs_full_notm}} or an external server.
{: shortdesc}

### Considerations and prerequisites
{: #prereqs-apiserver-logs}

Before you set up a Kubernetes API audit configuration, review the following information.




- **VPC clusters versions 4.15 and later**: Audit logs use the Red Hat OpenShift audit policy profile `default` (for default) and `WriteRequestBodies`(for verbose). For more information, see the [Audit log policy](https://docs.redhat.com/en/documentation/openshift_container_platform/4.15/html/security_and_compliance/audit-log-policy-config){: external}.

- **All other cluster versions**: Audit logs use the `openshift-audit` policy in the [`kube-samples` repo](https://github.com/IBM-Cloud/kube-samples/blob/master/kube-audit/openshift-audit-policy.yaml){: external}{: external}.





You can't modify the default policy or apply your own custom policy.
{: note}

* For Kubernetes audit logs and verbosity, see the [Kubernetes documentation](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/){: external}.
* Only one audit webhook can be created in a cluster.
* You must have the  [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the {{site.data.keyword.openshiftlong_notm}} cluster.

To get started, follow the instructions to send Kubernetes API audit logs [to a resource in the {{site.data.keyword.cloud_notm}} private network](#audit-api-server-priv).



### Forwarding Kubernetes API audit logs to Cloud Logs
{: #audit-api-server-la}

To forward audit logs to {{site.data.keyword.logs_full_notm}}, you can create a Kubernetes audit system by using the provided image and deployment.
{: shortdesc}

The following example uses the `icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs` image to forward logs to {{site.data.keyword.logs_full_notm}}. This image is usable as a production solution when configured [correctly](#prod-ready-deployment). For a more automated solution, configure and maintain your own log forwarding image.
{: important}

Previously the, `icr.io/ibm/ibmcloud-kube-audit-to-logdna` was used to forward logs. This image is deprecated and support ends soon. Update your log forwarding setup to use the `icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs` instead.
{: note}

The Kubernetes audit system in your cluster consists of an audit webhook, a log collection service and web server app, and a logging agent. The webhook collects the Kubernetes API server events from your cluster master. The log collection service is a Kubernetes `ClusterIP` service that is created from an image from the public {{site.data.keyword.cloud_notm}} registry. This service exposes a simple HTTP web server app that is exposed only on the cluster's network. The web server app parses the log data from the audit webhook and creates each log as a unique JSON line. Finally, the logging agent forwards the logs from the web server app to {{site.data.keyword.logs_full_notm}}, where you can view the logs.

**Before you begin**: Ensure that you reviewed the [considerations and prerequisites](#prereqs-apiserver-logs) and that you have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/account?topic=account-userroles) for {{site.data.keyword.logs_full_notm}}.

1. Target the global container registry for public {{site.data.keyword.cloud_notm}} images.
    ```sh
    ibmcloud cr region-set global
    ```
    {: pre}

2. Optional: For more information about the `kube-audit` image, inspect `icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs`.
    ```sh
    ibmcloud cr image-inspect icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs
    ```
    {: pre}
    
3. Set up your kubeconfig to access your cluster with
    ```sh
    ibmcloud ks cluster config -c <cluster>
    ```
    {: pre}

4. Create a configuration file named `ibmcloud-kube-audit.yaml`. This configuration file creates a log collection service and a deployment that pulls the `icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs` image to create a log collection container. {: #apply-deployment}

    
  
    ```yaml
    apiVersion: v1
    kind: List
    metadata:
      name: ibmcloud-kube-audit
    items:
      - apiVersion: v1
        kind: Namespace
        metadata:
          name: ibm-kube-audit
          labels:
            pod-security.kubernetes.io/enforce: restricted
            pod-security.kubernetes.io/enforce-version: latest
            pod-security.kubernetes.io/audit: restricted
            pod-security.kubernetes.io/audit-version: latest
            pod-security.kubernetes.io/warn: restricted
            pod-security.kubernetes.io/warn-version: latest
            security.openshift.io/scc.podSecurityLabelSync: "false"
      - apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: ibmcloud-kube-audit
          namespace: ibm-kube-audit
          labels:
            app: ibmcloud-kube-audit
        spec:
          replicas: 1
          selector:
            matchLabels:
              app: ibmcloud-kube-audit
          template:
            metadata:
              labels:
                app: ibmcloud-kube-audit
            spec:
              containers:
                - name: ibmcloud-kube-audit
                  image: 'icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs:latest'
                  imagePullPolicy: Always
                  ports:
                    - containerPort: 3000
                    - containerPort: 4443
                  securityContext:
                    allowPrivilegeEscalation: false
                    runAsNonRoot: true
                    capabilities:
                      drop:
                      - ALL
                    seccompProfile:
                      type: RuntimeDefault
                  volumeMounts:
                    - mountPath: /certificates
                      name: certificates
                      readOnly: true
              volumes:
                - name: certificates
                  secret:
                    secretName: audit-webhook
                    optional: true
      - apiVersion: v1
        kind: Service
        metadata:
          name: ibmcloud-kube-audit-service
          namespace: ibm-kube-audit
          labels:
            app: ibmcloud-kube-audit
        spec:
          selector:
            app: ibmcloud-kube-audit
          ports:
            - name: http
              protocol: TCP
              port: 80
              targetPort: 3000
            - name: https
              protocol: TCP
              port: 443
              targetPort: 4443
          type: ClusterIP
      - kind: NetworkPolicy
        apiVersion: networking.k8s.io/v1
        metadata:
          name: ibmcloud-kube-audit
          namespace: ibm-kube-audit
        spec:
          podSelector:
            matchLabels:
              app: ibmcloud-kube-audit
          policyTypes:
          - Ingress
          ingress:
          - ports:
            - protocol: TCP
              port: 3000
            - protocol: TCP
              port: 4443
            from:
            - namespaceSelector:
                matchLabels:
                  kubernetes.io/metadata.name: kube-system
              podSelector:
                matchLabels:
                  app: konnectivity-agent
            - namespaceSelector:
                matchLabels:
                  kubernetes.io/metadata.name: kube-system
              podSelector:
                matchLabels:
                  app: vpn
    ```
    {: codeblock}
  
    

5. Create the deployment in the `ibm-kube-audit` namespace of your cluster.
    ```sh
    kubectl apply -f ibmcloud-kube-audit.yaml
    ```
    {: pre}

6. Wait for the `ibmcloud-kube-audit` deployment to reach **Available**.
    ```sh
    kubectl wait --for condition=Available --namespace ibm-kube-audit --timeout 5m deploy/ibmcloud-kube-audit
    ```
    {: pre}

    Example output

    ```sh
    deployment.apps/ibmcloud-kube-audit condition met
    ```
    {: screen}

7. Verify that the `ibmcloud-kube-audit-service` service is deployed in your cluster.
    ```sh
    kubectl get svc -n ibm-kube-audit -l app=ibmcloud-kube-audit
    ```
    {: pre}

    Example output

    ```sh
    NAME                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
    ibmcloud-kube-audit-service   ClusterIP   172.21.xxx.xxx   <none>        80/TCP           1m
    ```
    {: screen}

8. For a production-ready deployment, [prepare that now](#prod-ready-deployment). If you do not require a production solution, skip this step.

9. Check the certificate authority status. If your certificates are nearing expiration, follow the steps to [rotate your certificates](/docs/openshift?topic=openshift-cert-rotate).
    ```sh
    ibmcloud oc cluster ca status -c <cluster>
    ```
    {: pre}
    
10. Save the `certificate-authority` of the cluster to file `cluster-ca.pem`. {: #query-cert}
    ```sh
    ibmcloud oc cluster ca get -c <cluster> --output json | jq -r .caCert | base64 -D > cluster-ca.pem
    ```
    {: pre}

11. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster) Prepare a certificate-based kubeconfig and save it to `kubeconfig.json`. Make sure to specify the `--admin` option to download the `client-certificate` and the `client-key` data to your local machine. This data is used later to configure the audit webhook.
    ```sh
    ibmcloud oc cluster config --cluster <cluster> --admin --output json > kubeconfig.json
    ```
    {: pre}

12. Extract the kubeconfig's client certificate to file `kubeconfig-cert.pem`.
    ```sh
    jq -r '.users[].user."client-certificate-data"' kubeconfig.json | base64 -D > kubeconfig-cert.pem
    ```
    {: pre}

13. Extract the kubeconfig's client key to file `kubeconfig-key.pem`.
    ```sh
    jq -r '.users[].user."client-key-data"' kubeconfig.json | base64 -D > kubeconfig-key.pem
    ```
    {: pre}

14. Configure the audit webhook and specify the `certificate-authority`, `client-certificate`, and `client-key`. The `certificate-authority` was retrieved in [step 10](#query-cert) and the`client-certificate` and `client-key` were retrieved in the previous two steps. Optionally configure the `policy` to a different value.
    ```text
    ibmcloud oc cluster master audit-webhook set \
        --cluster CLUSTER \
        --remote-server https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/http:ibmcloud-kube-audit-service:http/proxy/post \
        --ca-cert cluster-ca.pem \
        --client-cert kubeconfig-cert.pem \
        --client-key kubeconfig-key.pem \
        --policy default
    ```
    {: pre}
    
    For a production solution and after completing production-ready preparations in [step 8](#prod-ready-deployment), set `remote-server` to this `https` URL instead:
    {: note}
    
    ```sh
    https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/https:ibmcloud-kube-audit-service:https/proxy/post
    ```
    {: pre}

15. Verify that the audit webhook is created in your cluster.
    ```sh
    ibmcloud oc cluster master audit-webhook get --cluster <cluster>
    ```
    {: pre}

    Example output

    ```sh
    Server:   https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/http:ibmcloud-kube-audit-service:http/proxy/post
    Policy:   default 
    ```
    {: screen}

16. Apply the webhook to your Kubernetes API server by refreshing the cluster master. It might take several minutes for the master to refresh.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster>
    ```
    {: pre}

17. While the master refreshes, [provision an instance of {{site.data.keyword.logs_full_notm}} and deploy a logging agent to every worker node in your cluster](/docs/cloud-logs?topic=cloud-logs-kube2logs). The logging agent is required to forward logs from inside your cluster to the {{site.data.keyword.logs_full_notm}} service. If you already set up logging agents in your cluster, you can skip this step.

18. View the cluster's state and wait for the `Master State` to indicate `updating`, then wait for state `deployed`. It might take several minutes to complete.
    ```sh
    ibmcloud ks cluster get -c <cluster>
    ```
    {: pre}

    Example output

    ```sh
    ...
    Master
    Status:     Refresh in progress. (2 seconds ago)
    State:      updating
    ...
    Master
    Status:     Ready (2 seconds ago)
    State:      deployed
    ```
    {: screen}

19. After the master refresh completes and the logging agents are running on your worker nodes, you can [view your Kubernetes API audit logs in {{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-instance-launch).

After you set up the audit webhook in your cluster, you can monitor version updates to the `ibmcloud-kube-audit-to-ibm-cloud-logs` image by running `ibmcloud cr image-list --include-ibm | grep ibmcloud-kube-audit-to-ibm-cloud-logs`. To see the version of the image that currently runs in your cluster, run `oc get pods | grep ibmcloud-kube-audit-to-ibm-cloud-logs` to find the audit pod name, and run `kubectl describe pod <pod_name>` to see the image version.
Update the pod to the latest available on the current tag with `kubectl rollout restart --namespace ibm-kube-audit deploy/ibmcloud-kube-audit` and wait for the new pods to become available with `kubectl rollout status --timeout 1m --namespace ibm-kube-audit deploy/ibmcloud-kube-audit`.
{: tip}


### Production-ready deployment preparation
{: #prod-ready-deployment}

A few important things to note before preparing to forward logs:

1. The image tag `icr.io/ibm/ibmcloud-kube-audit-to-ibm-cloud-logs:latest` does receive vulnerability and bug fix updates. However, the deployment must be restarted manually to pick up those changes. Use `kubectl rollout restart -n ibm-kube-audit deploy/ibmcloud-kube-audit` to pull the latest image and gracefully restart.
2. This deployment is manually installed and managed. Switching from this deployment to another may result in audit log downtime.
3. The certificate generated below can be rotated. Rotation requires manual steps to replace the secret and restart the deployment.

To prepare the production-ready deployment, a private key and TLS certificate signed by the kube-apiserver are required.

1. After applying the YAML file in [step 4](#apply-deployment), wait for the Service resource to populate the cluster IP. Save that to the shell variable `$cluster_ip`.
    ```sh
    cluster_ip=$(
        kubectl wait \
            --for jsonpath='{.spec.clusterIP}' \
            --namespace ibm-kube-audit \
            --output jsonpath='{.spec.clusterIP}' \
            --timeout 5m \
            svc/ibmcloud-kube-audit-service
    )
    ```
    {: pre}
    
2. Generate a private key and save to `server.key`
    ```sh
    openssl genrsa -out server.key 4096
    ```
    {: pre}
    
3. Generate a Certificate Signing Request configuration file `server-csr.conf`. This is used to generate the certificate Kubernetes will sign.
    ```sh
    cat <<EOF > server-csr.conf
    [ req ]
    default_bits = 2048
    prompt = no
    default_md = sha256
    req_extensions = req_ext
    distinguished_name = dn

    [ dn ]
    CN = system:node:ibmcloud-kube-audit-service.ibm-kube-audit.svc
    O = system:nodes

    [ req_ext ]
    subjectAltName = @alt_names

    [ alt_names ]
    DNS.1 = ibmcloud-kube-audit-service.ibm-kube-audit.svc.cluster.local
    DNS.2 = ibmcloud-kube-audit-service.ibm-kube-audit.svc
    IP.1 = ${cluster_ip}
    EOF
    ```
    {: pre}
    
4. Generate the Certificate Signing Request payload for Kubernetes to sign.
    ```sh
    openssl req -new -config server-csr.conf -key server.key -out server.csr
    ```
    {: pre}
    
5. Insert the payload into a Kubernetes CertificateSigningRequest (CSR) resource
    ```sh
    kubectl apply -f - <<EOF
    apiVersion: certificates.k8s.io/v1
    kind: CertificateSigningRequest
    metadata:
      name: ibmcloud-kube-audit-service.ibm-kube-audit
    spec:
      request: $(base64 < server.csr | tr -d '\n')
      signerName: kubernetes.io/kubelet-serving
      usages:
      - digital signature
      - key encipherment
      - server auth
    EOF
    ```
    {: pre}
    
6. Approve the request
    ```sh
    kubectl certificate approve ibmcloud-kube-audit-service.ibm-kube-audit
    ```
    {: pre}
    
7. Wait for the certificate to be signed
    ```sh
    kubectl wait \
        --for jsonpath='{.status.certificate}' \
        --output go-template='{{.status.certificate | base64decode}}' \
        --timeout 5m \
        csr/ibmcloud-kube-audit-service.ibm-kube-audit > server.crt
    ```
    {: pre}
    
8. Create a Secret from the certificate and private key
    ```sh
    kubectl create secret tls \
        --cert server.crt \
        --key server.key \
        --namespace ibm-kube-audit \
        audit-webhook
    ```
    {: pre}
    
9. Restart the deployment to pick up the new secret.
    ```sh
    kubectl rollout restart --namespace ibm-kube-audit deploy/ibmcloud-kube-audit
    ```
    {: pre}
    
10. Wait for the new pods to become available
    ```sh
    kubectl rollout status --timeout 1m --namespace ibm-kube-audit deploy/ibmcloud-kube-audit
    ```
    {: pre}
    
11. The audit webhook is now ready to receive events over an encrypted connection. When configuring the audit webhook in the full guide above, you must use the `https` version of the `--remote-server` URL instead:
    ```txt
    https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/https:ibmcloud-kube-audit-service:https/proxy/post`
    ```
    {: pre}


### Forwarding Kubernetes API audit logs to a resource in the {{site.data.keyword.cloud_notm}} private network
{: #audit-api-server-priv}

Forward audit logs to a resource other than {{site.data.keyword.logs_full_notm}} that is outside of your cluster and accessible in the {{site.data.keyword.cloud_notm}} private network.
{: shortdesc}

The following example uses the `haproxytech/haproxy-alpine:2.6` image to forward logs. This image is for demonstration purposes only and should not be used in production environments. For a production solution, configure and maintain your own log forwarding image.
{: important}

Before you begin, ensure that you reviewed the [considerations and prerequisites](#prereqs-apiserver-logs).

1. Create a new directory `kube-audit-forwarder` and create a file `haproxy.cfg` in it with the following contents. Do not forget to replace `<REMOTE-IP>:<REMOTE-PORT>` in the file to the IP address and port of your remote log consumer.
    ```sh
    global
      log stdout format raw local0 info
    defaults
      mode http
      timeout client 10s
      timeout connect 5s
      timeout server 10s
      timeout http-request 10s
      log global
    frontend myfrontend
      bind :3000
      default_backend remotelogstash
    # Use remote log consumer IP and port here
    backend remotelogstash
      server s1 <REMOTE-IP>:<REMOTE-PORT> check
    ```
    {: codeblock}

    If your log consumer server is enforcing secure connection (TLS), you can add your certificate files to this directory and change the backend section in `haproxy.cfg` to use these files. For more information, see the [HAProxy documentation](https://haproxy-ingress.github.io/docs/){: external}.
    {: tip}

2. Create a configmap from the contents of `kube-audit-forwarder` directory.
    ```sh
    kubectl create namespace ibm-kube-audit; kubectl create configmap -n ibm-kube-audit kube-audit-forwarder-cm --from-file=kube-audit-forwarder
    ```
    {: pre}

3. Create a configuration file that is named `kube-audit-forwarder-remote-private-ip.yaml`. This configuration file creates a deployment and a service that forwards audit logs from the cluster to the IP address of the remote resource through the {{site.data.keyword.cloud_notm}} private network.
    ```yaml
    kind: Deployment
    apiVersion: apps/v1
    metadata:
      labels:
        app: kube-audit-forwarder
      name: kube-audit-forwarder
      namespace: ibm-kube-audit
    spec:
      revisionHistoryLimit: 2
      selector:
        matchLabels:
          app: kube-audit-forwarder
      strategy:
        rollingUpdate:
          maxUnavailable: 1
        type: RollingUpdate
      template:
        metadata:
          labels:
            app: kube-audit-forwarder
        spec:
          containers:
          - image: haproxytech/haproxy-alpine:2.6
            imagePullPolicy: IfNotPresent
            name: haproxy
            volumeMounts:
            - name: config-volume
              mountPath: /usr/local/etc/haproxy/haproxy.cfg
              subPath: haproxy.cfg
          volumes:
          - name: config-volume
            configMap:
              name: kube-audit-forwarder-cm
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: kube-audit-forwarder
      namespace: ibm-kube-audit
    spec:
      selector:
        app: kube-audit-forwarder
      ports:
        - protocol: TCP
          port: 80
          targetPort: 3000
    ---
    kind: NetworkPolicy
    apiVersion: networking.k8s.io/v1
    metadata:
      name: kube-audit-forwarder
      namespace: ibm-kube-audit
    spec:
      podSelector:
        matchLabels:
          app: kube-audit-forwarder
      policyTypes:
      - Ingress
      ingress:
      - ports:
        - protocol: TCP
          port: 3000
        from:
        - namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: kube-system
          podSelector:
            matchLabels:
              k8s-app: konnectivity-agent
        - namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: kube-system
          podSelector:
            matchLabels:
              app: konnectivity-agent
        - namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: kube-system
          podSelector:
            matchLabels:
              app: vpn
    ```
    {: codeblock}

    If you added certificate files to the `kube-audit-forwarder` in the previous step, do not forget to list those files in `volumeMounts` section as a `subPath`.
    {: tip}

4. Create the deployment and service.
    ```sh
    kubectl create -f kube-audit-forwarder-remote-private-ip.yaml
    ```
    {: pre}

5. Verify that the `kube-audit-forwarder` deployment and service is deployed in your cluster.
    ```sh
    kubectl get svc -n ibm-kube-audit
    ```
    {: pre}

    Example output

    ```sh
    NAME                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
    ...
    kube-audit-forwarder  ClusterIP   10.xxx.xx.xxx   <none>        80/TCP           1m
    ```
    {: screen}

    ```sh
    kubectl get deployment -n ibm-kube-audit
    ```
    {: pre}

    Example output

    ```sh
    NAME                   READY   UP-TO-DATE   AVAILABLE   AGE
    ...
    kube-audit-forwarder   1/1     1            1           6m27s
    ```
    {: screen}

6. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster) Make sure to specify the `--admin` option to download the `client-certificate` and the `client-key` files to your local machine. These files are used later to configure the audit webhook.
    ```sh
    ibmcloud oc cluster config --cluster <cluster> --admin
    ```
    {: pre}

7. Check the certificate authority status. If your certificates are nearing expiration, follow the steps to [rotate your certificates](/docs/openshift?topic=openshift-cert-rotate).
    ```sh
    ibmcloud oc cluster ca status -c CLUSTER
    ```
    {: pre}
    
8. Query the `certificate-authority` of the cluster and save it into a file.
   ```sh
    ibmcloud oc cluster ca get -c <cluster> --output json | jq -r .caCert | base64 -D > <certificate-authority>
    ```
    {: pre}

9. View your current config by running the `oc config view` command and review the output for the `client-certificate` and `client-key`.
    ```sh
    oc config view --minify
    ```
    {: pre}
    
    Example output
    
    ```sh
    clusters:
    - cluster:
        ...
        ...
        client-certificate: /Users/user/.bluemix/plugins/container-service/clusters/cluster-name-a111a11a11aa1aa11a11-admin/admin.pem
        client-key: /Users/user/.bluemix/plugins/container-service/clusters/cluster-name-a111a11a11aa1aa11a11-admin/admin-key.pem
    ```
    {: screen}

10. Configure the audit webhook and specify the `certificate-authority`, `client-certificate`, and `client-key` that you retrieved in the steps 5-7.
    ```sh
    ibmcloud oc cluster master audit-webhook set --cluster <cluster> --remote-server https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/kube-audit-forwarder/proxy/post --ca-cert <certificate-authority> --client-cert <client-certificate> --client-key <client-key> [--policy default|verbose]
    ```
    {: pre}

11. Verify that the audit webhook is created in your cluster.
    ```sh
    ibmcloud oc cluster master audit-webhook get --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output

    ```sh
    OK
    Server:            https://127.0.0.1:2040/api/v1/namespaces/ibm-kube-audit/services/kube-audit-forwarder/proxy/post
    Policy:            default
    ```
    {: screen}

12. Apply the webhook to your Kubernetes API server by refreshing the cluster master. The master might take several minutes to refresh.
    ```sh
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

After the master refresh completes, your logs are sent to the private IP address of your logging resource.





## Worker node audit logs
{: #audit-worker}

{{site.data.keyword.openshiftlong_notm}} uses the Linux Auditing System component, `auditd`, to monitor and log activity on the worker nodes. Although worker node auditing is enabled by default, no auditing data is available until you set up log forwarding to an {{site.data.keyword.logs_full_notm}} instance or external server.
{: shortdesc}

### Understanding the worker node audit configuration
{: #audit-worker-config}

The logs are stored in the `/var/log/audit` directory on the worker nodes. You can view the logs in {{site.data.keyword.logs_full_notm}} or your external server after you set up log forwarding.
{: shortdesc}

`Auditd` collects logs on various events, including the following:
- Linux system calls (`syscalls`)
- SELinux denials
- SELinux policy modifications
- Software modifications through the `yum` package installer
- `Systemd` operations
- Linux user and group modifications
- `Netfilter` change modifications 
- SSH Logins

### Setting up log forwarding for worker nodes
{: #audit-worker-setup}

See [Forwarding logs to an {{site.data.keyword.logs_full_notm}} instance](/docs/containers?topic=containers-health).
{: shortdesc}



## Service audit logs
{: #audit-service}

By default, {{site.data.keyword.openshiftlong_notm}} generates and sends events to {{site.data.keyword.logs_full_notm}}. To see these events, you must create an {{site.data.keyword.logs_full_notm}} instance. For more information, see [{{site.data.keyword.logs_full_notm}} events](/docs/openshift?topic=openshift-at_events_ref).



### Viewing `AuditWebhookError` alerts in auditing-enabled clusters
{: #audit-webhook-error-410}

{{site.data.keyword.openshiftlong_notm}} clusters version have an `AuditWebhookError` alert that fires when the audit webhook crashes or is deleted.
{: shortdesc}

To view the alert:

[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. From the {{site.data.keyword.openshiftshort}}, select the **Administrator** view.
1. Click **Observe** > **Alerting** > **AuditWebhookError**.
1. To create a notification for this alert, see [Sending notifications to external systems](https://docs.redhat.com/en/documentation/openshift_container_platform/4.10/html/monitoring/managing-alerts#sending-notifications-to-external-systems_managing-alerts){: external}.
