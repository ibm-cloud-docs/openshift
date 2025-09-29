---

copyright:
  years: 2025, 2025
lastupdated: "2025-09-29"


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
