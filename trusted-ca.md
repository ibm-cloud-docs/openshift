---

copyright:
  years: 2026, 2026
lastupdated: "2026-03-26"

keywords: openshift, red hat, red hat openshift, roks, trusted ca, certificate authority, ca bundle, hypershift

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Adding a trusted CA to {{site.data.keyword.openshiftlong_notm}}
{: #trusted-ca}

[Virtual Private Cloud]{: tag-vpc}
[4.19 and later]{: tag-warm-gray}
[RHCOS worker nodes]{: tag-magenta}
[RHEL worker nodes]{: tag-red}

Learn how to add a trusted Certificate Authority (CA) to your {{site.data.keyword.openshiftlong}} cluster. You might need to add a trusted CA when pulling images from a self-hosted registry that uses a certificate signed by a custom CA.
{: shortdesc}

## Adding a trusted CA to your cluster
{: #trusted-ca-install}

To add a trusted CA to your {{site.data.keyword.openshiftlong_notm}} cluster, you create a configmap containing your CA certificate and deploy a daemonset that installs the certificate on all worker nodes.

Before you begin, ensure you have your CA certificate file ready. The certificate must be in PEM format.

1. Create the `openshift-config-user-ca-bundle` configmap with your CA certificate. Replace `<path-to-your-ca-cert>` with the path to your CA certificate file.

    ```sh
    kubectl create cm openshift-config-user-ca-bundle -n kube-system --from-file=openshift-config-user-ca-bundle.crt=<path-to-your-ca-cert>
    ```
    {: pre}

1. Create the script that installs the trusted CA on each node.

    ```sh
    cat > openshift-config-user-ca-script.sh <<EOF
    #!/bin/bash
    set -e  # Exit on any error
    set -x  # Enable debug output
    if ! diff /tmp/openshift-config-user-ca-bundle/openshift-config-user-ca-bundle.crt /host/etc/pki/ca-trust/source/anchors ; then
        cp /tmp/openshift-config-user-ca-bundle/openshift-config-user-ca-bundle.crt /host/etc/pki/ca-trust/source/anchors
        chroot /host update-ca-trust extract
        if chroot /host systemctl is-enabled coreos-update-ca-trust.service; then
            chroot /host systemctl restart coreos-update-ca-trust.service
        fi
        chroot /host systemctl restart crio.service;
    fi
    # Keep container running to maintain daemonset pod
    sleep inf
    EOF
    kubectl delete cm -n kube-system openshift-config-user-ca-script --ignore-not-found
    kubectl create cm -n kube-system --from-file openshift-config-user-ca-script.sh openshift-config-user-ca-script
    ```
    {: pre}

1. Create the daemonset that runs the script on all nodes.

    ```sh
    OCP_REGISTRY_ENDPOINT=$(kubectl get pod -n kube-system -l k8s-app=kube-apiserver-proxy -o json | jq -r '.items[0].spec.containers[0].image | select( . != null )' | awk -F/ '{ print $1 }')
    if [[ -z "${OCP_REGISTRY_ENDPOINT}" ]]; then
        OCP_REGISTRY_ENDPOINT=$(kubectl get pod -n kube-system -l app=ibm-master-proxy-static -o json | jq -r '.items[0].spec.containers[0].image | select( . != null )' | awk -F/ '{ print $1 }')
    fi
    OCP_VERSION=$(oc version -o json | jq -r .openshiftVersion)
    kubectl apply -f - <<EOF
    ---
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      name: update-openshift-config-user-ca-bundle
      namespace: kube-system
      labels:
        app: update-openshift-config-user-ca-bundle
    spec:
      selector:
        matchLabels:
          app: update-openshift-config-user-ca-bundle
      template:
        metadata:
          labels:
            app: update-openshift-config-user-ca-bundle
        spec:
          containers:
            - command: ["/bin/bash", "-c", "/tmp/openshift-config-user-ca-script/openshift-config-user-ca-script.sh"]
              image: ${OCP_REGISTRY_ENDPOINT}/armada-master/ocp-release-${OCP_VERSION}-x86_64:cli
              imagePullPolicy: IfNotPresent
              name: update-openshift-config-user-ca-bundle
              resources:
                requests:
                  cpu: 1m
                  memory: 1Mi
              securityContext:
                privileged: true
              volumeMounts:
                - name: host-volume
                  mountPath: /host
                - name: openshift-config-user-ca-bundle
                  mountPath: /tmp/openshift-config-user-ca-bundle
                - name: openshift-config-user-ca-script
                  mountPath: /tmp/openshift-config-user-ca-script
          hostIPC: true
          hostNetwork: true
          hostPID: true
          tolerations:
          - operator: Exists
          volumes:
            - name: host-volume
              hostPath:
                path: /
                type: Directory
            - name: openshift-config-user-ca-bundle
              configMap:
                name: openshift-config-user-ca-bundle
            - name: openshift-config-user-ca-script
              configMap:
                name: openshift-config-user-ca-script
                defaultMode: 0755
    EOF
    kubectl rollout status ds -n kube-system update-openshift-config-user-ca-bundle
    ```
    {: pre}

1. Verify that the trusted CA was installed by checking the daemonset logs.

    ```sh
    oc logs -n kube-system -l app=update-openshift-config-user-ca-bundle --tail=-1
    ```
    {: pre}

After the daemonset completes, your trusted CA is installed on all worker nodes and your cluster can pull images from registries that use certificates signed by your custom CA.

