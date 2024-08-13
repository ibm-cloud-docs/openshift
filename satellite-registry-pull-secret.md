---

copyright:
  years: 2023, 2024
lastupdated: "2024-08-13"


keywords: openshift, satellite, distributed cloud, on-prem, hybrid, images, private registry, pull secret

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Updating the global pull secret in {{site.data.keyword.satelliteshort}} clusters
{: #satellite-registry-pull-secret}

After setting up a {{site.data.keyword.satelliteshort}} cluster, you can update the global pull secret in your cluster to pull from a private container registry other than `quay.io` or `icr.io`. For example, you might want to pull images from the Cloud Pak Entitled Registry (`cp.icr.io`) or your own private registry.
{: shortdesc}

There are two ways to update the global pull secret in Satellite clusters.

[Updating the global pull secret](#satellite-pull-secret-cli).
:   Use this approach if you have one or few clusters to maintain. You must repeat these steps for each cluster where you want to apply the secret.

[Updating the global pull secret by using {{site.data.keyword.satelliteshort}} config](#satellite-pull-secret-config). 
:   Use this approach if you maintain several {{site.data.keyword.satelliteshort}} clusters and cluster groups. By using {{site.data.keyword.satelliteshort}} config, you can apply the secret changes across your {{site.data.keyword.satelliteshort}} clusters and cluster groups.

## Updating the global pull secret
{: #satellite-pull-secret-cli}

Complete the following steps to update the global pull secret in your {{site.data.keyword.satelliteshort}} cluster.


1. Create a secret that has the credentials for the registry you want to use.
    ```sh
    oc create secret docker-registry docker-auth-secret \
    --docker-server=REGISTRY \
    --docker-username=USERNAME \
    --docker-password=PASSWORD \
    --namespace kube-system
    ```
    {: pre}

    Example `create secret` command for using the Cloud Pak Entitled Registry.
    ```sh
    oc create secret docker-registry docker-auth-secret \
    --docker-server=cp.icr.io \
    --docker-username=cp \
    --docker-password=ENTITLEMENT-KEY \
    --namespace kube-system
    ```
    {: pre}

1. Create a DaemonSet to apply the secret across all worker nodes.
    ```yaml
    cat << EOF | oc create -f -
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      name: update-docker-config
      namespace: kube-system
      labels:
        app: update-docker-config
    spec:
      selector:
        matchLabels:
          name: update-docker-config
      template:
        metadata:
          labels:
            name: update-docker-config
        spec:
          initContainers:
            - command: ["/bin/sh", "-c"]
              args:
                - >
                  echo "Checking if RHEL or RHCOS host";
                  [[ -s /docker-config/.docker/config.json  ]] && CONFIG_PATH=/docker-config/.docker || CONFIG_PATH=/docker-config/root/.docker;
                  echo "Backing up or restoring config.json";
                  [[ -s \$CONFIG_PATH/config.json ]] && cp \$CONFIG_PATH/config.json \$CONFIG_PATH/config.json.bak || cp \$CONFIG_PATH/config.json.bak \$CONFIG_PATH/config.json;
                  echo "Merging secret with config.json";
                  /host/usr/bin/jq -s '.[0] * .[1]' \$CONFIG_PATH/config.json /auth/.dockerconfigjson > \$CONFIG_PATH/config.tmp;
                  mv \$CONFIG_PATH/config.tmp \$CONFIG_PATH/config.json;
                  echo "Sending signal to reload crio config";
                  pidof crio;
                  kill -1 \$(pidof crio)
              image: icr.io/ibm/alpine:latest
              imagePullPolicy: IfNotPresent
              name: updater
              resources: {}
              securityContext:
                privileged: true
              volumeMounts:
                - name: docker-auth-secret
                  mountPath: /auth
                - name: docker
                  mountPath: /docker-config
                - name: bin
                  mountPath: /host/usr/bin
                - name: lib64
                  mountPath: /lib64
          containers:
            - resources:
                requests:
                  cpu: 0.01
              image: icr.io/ibm/alpine:latest
              name: sleepforever
              command: ["/bin/sh", "-c"]
              args:
                - >
                  while true; do
                    sleep 100000;
                  done
          hostPID: true
          volumes:
            - name: docker-auth-secret
              secret:
                secretName: docker-auth-secret
            - name: docker
              hostPath:
                path: /
            - name: bin
              hostPath:
                path: /usr/bin
            - name: lib64
              hostPath:
                path: /lib64
                hostPathType: Directory
    EOF
    ```
    {: codeblock}

1. Verify the pods are running.
    ```sh
    oc get daemonset -n kube-system update-docker-config
    ```
    {: pre}

## Updating the global pull secret by using {{site.data.keyword.satelliteshort}} config
{: #satellite-pull-secret-config}

Complete the following steps to use {{site.data.keyword.satelliteshort}} config to apply the global pull secret across your {{site.data.keyword.satelliteshort}} clusters and cluster groups.

1. [Make sure you enable {{site.data.keyword.satelliteshort}} config](/docs/satellite?topic=satellite-setup-clusters-satconfig).
1. [Add your clusters to cluster groups](/docs/satellite?topic=satellite-setup-clusters-satconfig-groups).
1. Create a secret in one of your {{site.data.keyword.satelliteshort}} clusters. Note that this secret will be deleted later.
    ```sh
    oc create secret docker-registry docker-auth-secret \
    --docker-server=REGISTRY \
    --docker-username=USERNAME \
    --docker-password=PASSWORD \
    --namespace kube-system
    ```
    {: pre}

    Example `create secret` command for using the Cloud Pak Entitled Registry.
    ```sh
    oc create secret docker-registry docker-auth-secret \
    --docker-server=cp.icr.io \
    --docker-username=cp \
    --docker-password=ENTITLEMENT-KEY \
    --namespace kube-system
    ```
    {: pre}

1. Get the details of your secret. Copy and save the base64 encoded `dockerconfigjson` section.
    ```sh
    oc get secret docker-auth-secret -o yaml
    ```
    {: pre}

1. Delete the secret.
    ```sh
    oc delete secret docker-auth-secret -n kube-system
    ```
    {: pre}

1. Create a configuration file called `secret.yaml` that has your registry credentials. Paste the base64 encoded `dockerconfigjson` section that you saved in the earlier step.
    ```yaml
    kind: Secret
    apiVersion: v1
    metadata:
      name: docker-auth-secret
      namespace: kube-system
    data:
      .dockerconfigjson: >-
        BASE64-ENCODED-SECRET
    type: kubernetes.io/dockerconfigjson
    ```
    {: codeblock}

1. Create a {{site.data.keyword.satelliteshort}} config. In the `--data-location` option, specify the **Managed from** region of your Location.
    ```sh
    ibmcloud sat config create --data-location wdc --name my-config
    ```
    {: pre}

1. Add a version to your configuration. Specify the file path to the `secret.yaml` that you created earlier.
    ```sh
    ibmcloud sat config version create --name 1 --config my-config --file-format yaml --read-config /Users/username/Desktop/secret.yaml
    ```
    {: pre}

1. Create a subscription to apply the DaemonSet to a cluster group.
    ```sh
    ibmcloud sat subscription create --name my-subscription --config my-config --group GROUP
    ```
    {: pre}

1. Save the following DaemonSet to a file called `ds.yaml`.
    ```yaml
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      name: update-docker-config
      namespace: kube-system
      labels:
        app: update-docker-config
    spec:
      selector:
        matchLabels:
          name: update-docker-config
      template:
        metadata:
          labels:
            name: update-docker-config
        spec:
          initContainers:
            - command: ["/bin/sh", "-c"]
              args:
                - >
                  echo "Checking if RHEL or RHCOS host";
                  [[ -s /docker-config/.docker/config.json  ]] && CONFIG_PATH=/docker-config/.docker || CONFIG_PATH=/docker-config/root/.docker;
                  echo "Backing up or restoring config.json";
                  [[ -s \$CONFIG_PATH/config.json ]] && cp \$CONFIG_PATH/config.json \$CONFIG_PATH/config.json.bak || cp \$CONFIG_PATH/config.json.bak \$CONFIG_PATH/config.json;
                  echo "Merging secret with config.json";
                  /host/usr/bin/jq -s '.[0] * .[1]' \$CONFIG_PATH/config.json /auth/.dockerconfigjson > \$CONFIG_PATH/config.tmp;
                  mv \$CONFIG_PATH/config.tmp \$CONFIG_PATH/config.json;
                  echo "Sending signal to reload crio config";
                  pidof crio;
                  kill -1 \$(pidof crio)
              image: icr.io/ibm/alpine:latest
              imagePullPolicy: IfNotPresent
              name: updater
              resources: {}
              securityContext:
                privileged: true
              volumeMounts:
                - name: docker-auth-secret
                  mountPath: /auth
                - name: docker
                  mountPath: /docker-config
                - name: bin
                  mountPath: /host/usr/bin
                - name: lib64
                  mountPath: /lib64
          containers:
            - resources:
                requests:
                  cpu: 0.01
              image: icr.io/ibm/alpine:latest
              name: sleepforever
              command: ["/bin/sh", "-c"]
              args:
                - >
                  while true; do
                    sleep 100000;
                  done
          hostPID: true
          volumes:
            - name: docker-auth-secret
              secret:
                secretName: docker-auth-secret
            - name: docker
              hostPath:
                path: /
            - name: bin
              hostPath:
                path: /usr/bin
            - name: lib64
              hostPath:
                path: /lib64
                hostPathType: Directory
    ```
    {: codeblock}


1. Create a {{site.data.keyword.satelliteshort}} config. In the `--data-location` option, specify the **Managed from** region of your Location, for example `wdc`.
    ```sh
    ibmcloud sat config create --data-location wdc --name my-ds
    ```
    {: pre}

1. Add a version to your configuration. Specify the file path to the `ds.yaml` that you created earlier.
    ```sh
    ibmcloud sat config version create --name 1 --config my-ds --file-format yaml --read-config /Users/username/Desktop/ds.yaml
    ```
    {: pre}

1. Create a subscription to apply the DaemonSet to a cluster group.
    ```sh
    ibmcloud sat subscription create --name my-subscription --config my-ds --group GROUP
    ```
    {: pre}

1. Verify the secret and DaemonSet are deploy across your clusters.
    ```sh
    oc get secret docker-auth-secret -n kube-system
    ```
    {: pre}

    ```sh
    oc get ds update-docker-config -n kube-system
    ```
    {: pre}

You can also view and manage your configurations and subscriptions from the [{{site.data.keyword.satelliteshort}} console](https://cloud.ibm.com/satellite/locations){: external}.
{: tip}

