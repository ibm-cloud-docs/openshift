---

copyright:
  years: 2025, 2026
lastupdated: "2026-04-10"


keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}




# How do I troubleshoot confidential containers?
{: #ts-confidential-containers}
{: support}


Review these possible issues.
{: tsSymptoms}


The issues could be caused by a misconfiguration during setup.
{: tsCauses}


To start troubleshooting issues, run the following commands to gather as much data about your confidential containers as you can.
{: tsResolve}

1. Gather information about the operator.
    ```bash
    oc get csv -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    ```bash
    oc describe csv -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    ```bash
    oc get all -n openshift-sandboxed-containers-operator
    ```
    {: pre}

1. Retrieve logs and events from all pods related to the DaemonSets.

    ```bash
    oc describe pod/osc-caa-ds-<random string> -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    ```bash
    oc logs pod/osc-caa-ds-<random string> -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    ```bash
    oc describe pod/osc-config-sync-install-<random string> -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    ```bash
    oc logs pod/osc-config-sync-install-<random string> -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    ```bash
    oc describe pod/osc-rpm-install-<random string> -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    ```bash
    oc logs pod/osc-rpm-install-<random string> -n openshift-sandboxed-containers-operator
    ```
    {: pre}

1. Gather information about the pods.

    a. Gather information about the controller manager.

    ```bash
    oc describe pod/controller-manager-<random string> -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    ```bash
    oc logs pod/controller-manager-<random string> -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    b. Gather logs for a a random string.

    ```bash
    oc logs pod/<random string>
    ```
    {: pre}

    ```bash
    oc describe pod/<random string>
    ```
    {: pre}

    c. Gather information about the `openshift-sandboxed-containers-operator-bundle`.

    ```bash
    oc logs pod/trikprot-openshift-sandboxed-containers-operator-bundle-<version>
    ```
    {: pre}

    ```bash
    oc describe pod/trikprot-openshift-sandboxed-containers-operator-bundle-<version>
    ```
    {: pre}

1. Gather information about the ConfigMaps.

    a. Gather information about the feature gates.
    ```bash
    oc get configmap/osc-feature-gates -n openshift-sandboxed-containers-operator -o yaml
    ```
    {: pre}

    b. Gather information about the peer pods.
    ```bash
    oc get configmap/peer-pods-cm -n openshift-sandboxed-containers-operator -o yaml
    ```
    {: pre}

    c. Gather information about the secrets.

    ```bash
    oc get secret/auth-json-secret -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    ```bash
    oc get secret/peer-pods-secret -n openshift-sandboxed-containers-operator
    ```
    {: pre}

    d. Gather information about the KataConfig.

    ```bash
    oc get kataconfigs.kataconfiguration.openshift.io/kata-runtime-settings -n openshift-sandboxed-containers-operator -o yaml
    ```
    {: pre}

    e. Gather information about the Custom Resource Definitions.

    ```bash
    oc get crd/peerpods.confidentialcontainers.org
    ```
    {: pre}

    ```bash
    oc get crd/kataconfigs.kataconfiguration.openshift.io
    ```
    {: pre}

1. Check peer pods capacity and limits.

    a. Check the current peer pods limit across all worker nodes.

    ```bash
    oc get nodes -o json | jq -r '[.items[] | select (.status.allocatable["kata.peerpods.io/vm"] != null)| .status.allocatable["kata.peerpods.io/vm"] | tonumber] | add'
    ```
    {: pre}

    b. Check the allocated resources on each worker node.

    ```bash
    for n in $(oc get nodes -o name); do
      echo "=== $n ==="
      oc describe "$n" | sed -n '/Allocated resources:/,/Events:/p'
    done
    ```
    {: pre}

    c. Count the number of peer pods currently running.

    ```bash
    oc get pods -A -o json | jq '.items[] | select(.spec.runtimeClassName == "kata-remote") | "\(.metadata.namespace)/\(.metadata.name)"' | wc -l
    ```
    {: pre}

## Common issues and resolutions
{: #ts-confidential-containers-common}

### Insufficient kata.peerpods.io/vm error
{: #ts-conf-cont-insufficient-vm}

If you see an error like the following when scheduling peer pods:

```sh
Warning FailedScheduling 0/30 nodes are available: 9 Insufficient kata.peerpods.io/vm. preemption: 0/30 nodes are available: 9 No preemption victims found for incoming pod.
```

This error indicates that you have reached the `PEERPODS_LIMIT_PER_NODE` limit on your worker nodes. The default limit is 10 peer pods per worker node.

To resolve this issue:

1. Verify the current limit and how many peer pods are running.

    ```bash
    oc get nodes -o json | jq '.items[] | {name: .metadata.name, allocatable: .status.allocatable["kata.peerpods.io/vm"], capacity: .status.capacity["kata.peerpods.io/vm"]}'
    ```
    {: pre}

2. Increase the `PEERPODS_LIMIT_PER_NODE` value in the `peer-pods-cm` ConfigMap. For more information, see [Creating confidential containers](/docs/openshift?topic=openshift-confidential-containers).

    ```bash
    oc -n openshift-sandboxed-containers-operator patch cm peer-pods-cm \
      --type merge \
      -p '{"data":{"PEERPODS_LIMIT_PER_NODE":"24"}}'
    ```
    {: pre}

3. Restart the Cloud API Adapter daemonset.

    ```bash
    oc -n openshift-sandboxed-containers-operator rollout restart daemonset/osc-caa-ds
    ```
    {: pre}

4. Verify the new limit is applied.

    ```bash
    oc get nodes -o json | jq -r '[.items[] | select (.status.allocatable["kata.peerpods.io/vm"] != null)| .status.allocatable["kata.peerpods.io/vm"] | tonumber] | add'
    ```
    {: pre}

For more information about peer pods limits and capacity planning, see [How many peer pods can I run per worker node?](/docs/openshift?topic=openshift-faqs#conf-cont-peerpods-limit).

### Insufficient CPU error
{: #ts-conf-cont-insufficient-cpu}

If you see an error like the following when scheduling peer pods:

```sh
Warning FailedScheduling 0/3 nodes are available: 3 Insufficient cpu. preemption: 0/3 nodes are available: 3 No preemption victims found for incoming pod.
```

This error indicates that your worker nodes do not have enough CPU resources available. Each peer pod consumes approximately 250m CPU on the worker node for the Kubernetes pod construct, even though the actual workload runs in a separate VSI.

To resolve this issue:

1. Check the CPU allocation on your worker nodes.

    ```bash
    for n in $(oc get nodes -o name); do
      echo "=== $n ==="
      oc describe "$n" | sed -n '/Allocated resources:/,/Events:/p'
    done
    ```
    {: pre}

2. Choose one of the following options:

    - Add more worker nodes to your cluster
    - Use worker nodes with more vCPUs
    - Reduce the `PEERPODS_LIMIT_PER_NODE` value to match your worker node capacity
    - Remove other workloads from the worker nodes to free up CPU resources
