---
 
copyright:
  years: 2024, 2026
lastupdated: "2026-04-27"
 
 
keywords: openshift, sysdig, ebpf, rhcos, crashloopbackoff, monitoring
 
subcollection: openshift
content-type: troubleshoot
 
---
 
{{site.data.keyword.attribute-definition-list}}
 
 
 
 
# Why are `sysdig-agent` pods in `CrashLoopBackOff` on a private-only RHCOS cluster?
{: #ts-cluster-sysdig-ebpf}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[RHCOS worker nodes]{: tag-magenta}
[Private only]{: tag-dark-teal}

If your cluster uses RHCOS worker nodes and no outbound internet access, the `sysdig-agent` pods in the `ibm-observe` namespace might enter `CrashLoopBackOff` or fail to start.
{: shortdesc}

Your `sysdig-agent` pods are in `CrashLoopBackOff` or failing to start in the `ibm-observe` namespace on a private-only cluster that uses RHCOS worker nodes.
{: tsSymptoms}
 
You might see the `sysdig-agent` pods repeatedly restart and fail to become healthy after installing or configuring the Sysdig integration. When you check the pod logs, you see errors similar to the following:

```sh
oc -n ibm-observe logs <sysdig-agent-pod> --previous
```
{: pre}

Example output:
```sh
* Kernel headers not found in /host/lib/modules/5.14.0-427.105.1.el9_4.x86_64/build, continuing anyway
* Loading kernel probe
Error! Your kernel headers for kernel 5.14.0-427.105.1.el9_4.x86_64 cannot be found at /lib/modules/5.14.0-427.105.1.el9_4.x86_64/build or /lib/modules/5.14.0-427.105.1.el9_4.x86_64/source.
* Trying to download precompiled module from https://download.sysdig.com/stable/sysdig-probe-binaries/...
Download of sysdigcloud-probe for version 14.3.2 failed.
curl: (28) Failed to connect to download.sysdig.com port 443: Connection timed out
Cannot load the probe
```
{: screen}
 
On RHCOS worker nodes, the monitoring agent can't rely on local kernel headers because RHCOS does not include them. In this scenario, the Sysdig agent attempts to reach `sysdig.com` to retrieve a precompiled driver. In private-only clusters, or clusters without outbound internet access, this process fails and the agent pods can enter `CrashLoopBackOff`.
{: tsCauses}

If the eBPF driver is not enabled, this is a potential cause of the issue. Follow these steps to diagnose and resolve the problem.

eBPF is now enabled by default for new Sysdig deployments. However, if you are experiencing issues on an existing cluster with RHCOS workers in a private-only environment, verify whether eBPF is enabled and enable it if necessary.
 
 
Verify your Sysdig agent configuration and enable the eBPF driver if needed.
{: tsResolve}
 
1. Check if the eBPF driver is currently enabled on your cluster.
    ```sh
    oc -n ibm-observe get daemonset/sysdig-agent -o jsonpath='{.spec.template.spec.containers[0].env[?(@.name=="SYSDIG_AGENT_DRIVER")].value}'
    ```
    {: pre}

    - If the output shows `universal_ebpf`, eBPF is already enabled. The steps below are not necessary, and following them will cause no harm but will not resolve your issue. You may need to investigate other potential causes.
    - If the output is empty or shows a value other than `universal_ebpf`, continue to the next step to enable eBPF.

1. Set the Sysdig agent driver to `universal_ebpf`.
    ```sh
    oc -n ibm-observe set env daemonset/sysdig-agent SYSDIG_AGENT_DRIVER=universal_ebpf
    ```
    {: pre}

1. Restart the `sysdig-agent` pods.
    ```sh
    oc delete pods -l app=sysdig-agent -n ibm-observe
    ```
    {: pre}

1. Verify that the replacement pods are created and return to a `Running` state.
    ```sh
    oc get pods -l app=sysdig-agent -n ibm-observe
    ```
    {: pre}

For more information about monitoring limitations on RHCOS worker nodes, see [Monitoring cluster health](/docs/openshift?topic=openshift-health-monitor).
