---

copyright:
  years: 2014, 2021
lastupdated: "2021-11-10"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the DNS Operator show a `RouteHealthDegraded` or `cannot marshal DNS message` error?
{: #ingress_subdomain}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


You receive an error message similar to one of the following.
{: tsSymptoms}

**Example error message when installing {{site.data.keyword.icp4dfull_notm}} from the console**
```sh
XXX.us-south.containers.appdomain.cloud: Get "http://image-registry-openshift-image-registry.ocp-data-privacy-prod-c-XXX.us-south.containers.appdomain.cloud/v2/": dial tcp: lookup image-registry-openshift-image-registry.ocp-data-privacy-prod-c-XXX.us-south.containers.appdomain.cloud on XXX.XX.X.XX:XX: cannot marshal DNS message
```
{: screen}

**Example `nslookup` error**
```sh
# nslookup XXX.XXX.databases.appdomain.cloud
Server:        XXX.XX.X.XX
Address:    XXX.XX.X.XX:XX

Non-authoritative answer:
*** Can't find XXX.XXX.databases.appdomain.cloud: Parse error

Non-authoritative answer:
*** Can't find XXX.XXX.databases.appdomain.cloud: Parse error
```
{: screen}


The fix for [bug 1953097](https://bugzilla.redhat.com/show_bug.cgi?id=1970140){: external} enabled CoreDNS `bufsize` plug-in responses of `1232` bytes. Some DNS resolvers can't receive responses greater than `512` bytes. Note that DNS resolvers that retry lookups using TCP, such as Dig, are not impacted. DNS clients that do not require UDP DNS messages to exceed 512 bytes are not impacted.
{: tsCauses}

Update your cluster master and worker nodes.
{: tsResolve}

1. [Update your cluster master](/docs/openshift?topic=openshift-update#master). For 4.6 clusters, update your master to version `4.6.38_openshift` or later. For 4.7 clusters, update your master to version `4.7.19_openshift` or later.
    ```sh
    ibmcloud oc cluster master update --cluster <clusterID> --version <4.6.38_openshift|4.7.19_openshift>
    ```
    {: pre}

1. After you update your master, run the `cluster get` command to get the cluster state and version and verify that the state is `deployed`.
    ```sh
    ibmcloud oc cluster get --cluster <clusterID>
    ```
    {: pre}

1. [Update your worker nodes](/docs/openshift?topic=openshift-update#master). For 4.6 clusters, update your worker nodes to version `4.6.38_openshift` or later. For 4.7 clusters, update your worker nodes to version `4.7.19_openshift` or later.

1. Get the details of the `openshift-dns` configmap and review the `bufsize` by running the following command. 
    ```sh
    oc get configmap -n openshift-dns dns-default -o yaml
    ```
    {: pre}

1. If the `bufsize` is still `1232`, get the name of the DNS Operator pod.
    ```sh
    oc get pods -n openshift-dns-operator
    ```
    {: pre}

    **Example output**
    ```sh
    NAME READY STATUS RESTARTS AGE
    dns-operator-111aa1aaab-xxxx1 2/2 Running 0 5h49m
    ```
    {: screen}

1. Delete the DNS Operator pod.
    ```sh
    oc delete pod <dns_operator_pod> -n openshift-dns-operator 
    ```
    {: pre}

1. Wait for the DNS pod to restart. Run `get pods` with the `--watch` flag to to verify that the pod is deployed.
    ```sh
    oc get pods -n openshift-dns --watch
    ```
    {: pre}

1. Verify that the DNS Operator pod is running.
    ```sh
    oc get pods -n openshift-dns-operator
    ```
    {: pre}

1. Get the configmap YAML and verify that the the `bufsize` is `512`. 
    ```sh
    oc get configmap -n openshift-dns dns-default -o yaml
    ```
    {: pre}

1. After a few minutes, verify that the DNS resolution works. If you see an `nslookup` error, retry the `nslookup`.

    ```sh
    / # nslookup XXX.XXX.databases.appdomain.cloud
    Server:        XXX.XX.X.XX
    Address:    XXX.XX.X.XX:XX

    Non-authoritative answer:
    XXX.XXX.databases.appdomain.cloud    canonical name = icd-prod-us-south-db-lm0sr.us-south.containers.appdomain.cloud
    icd-prod-us-south-db-lm0sr.us-south.containers.appdomain.cloud    canonical name = icd-prod-us-south-db-lm0sr.XXX.akadns.net

    Non-authoritative answer:
    XXX.XXX.databases.appdomain.cloud    canonical name = icd-prod-us-south-db-lm0sr.us-south.containers.appdomain.cloud
    icd-prod-us-south-db-lm0sr.us-south.containers.appdomain.cloud    canonical name = icd-prod-us-south-db-lm0sr.XXX.akadns.net
    Name:    icd-prod-us-south-db-lm0sr.XXX.akadns.net
    Address: XXX.XX.XXX.XX
    Name:    icd-prod-us-south-db-lm0sr.XXX.akadns.net
    Address: XXX.XX.X.XX
    Name:    icd-prod-us-south-db-lm0sr.XXX.akadns.net
    Address: XXX.XX.XXX.XXX
    ```
    {: codeblock}










