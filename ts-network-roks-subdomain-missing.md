---

copyright:
  years: 2014, 2021
lastupdated: "2021-09-27"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---


{{site.data.keyword.attribute-definition-list}}
  

# Why is my cluster missing the public `containers.appdomain.cloud` subdomain?
{: #roks_ts_subdomain}
{: troubleshoot}
{: support}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC


When you expose an app through a router subdomain, you get a local subdomain instead of a public route, in the format: `<service_name>-<project_name>.router.default.svc.cluster.local`.
{: tsSymptoms}

When you try to open the {{site.data.keyword.openshiftshort}} web console or another app route in your browser, you might see an error similar to the following.

```
Application is not available
The application is currently not serving requests on this endpoint.
```
{: screen}


After the cluster is created and enters a **normal** state, the router subdomain networking and load balancing components still take some time to deploy.
{: tsCauses}

If you expose your app before the networking components fully provision, or if the components experience an error, your apps can only be exposed internally with the default router's `svc.cluster.local` domain.

When the components fully provision, a public router subdomain is available for your apps, in the format `<cluster-name>-<accountID-hashed>-<ssll>.<region>.containers.appdomain.cloud`.


1. After you create a cluster, wait some time before you expose your apps, even after the cluster enters a **normal** state.
{: tsResolve}

2. Check the **Master Status**. If the **Master Status** is not **Ready**, [review its status](/docs/openshift?topic=openshift-debug_master) and follow any troubleshooting information to resolve the issue.   
    ```
    ibmcloud oc cluster get -c <cluster_name_or_ID>
    ```
    {: pre}

3. Check that your cluster has public connectivity so that the networking components can talk to the master as they deploy.
    * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC clusters with public and private cloud service endpoints enabled: [Ensure that a public gateway is enabled on each subnet](/docs/openshift?topic=openshift-vpc-subnets#create_vpc_subnet) that your cluster is attached to. Public gateway are required for default components such as the web console and OperatorHub to use a secure, public connection to complete actions such as pulling images from remote, private registries. Note that if only the private service endpoint is enabled for your cluster, no public gateway is required because the private cloud service endpoint is used by default to access OpenShift components such as the OpenShift web console or OperatorHub.
    * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic clusters:
        * In the output of Step 2, check that your cluster has a **Public Service Endpoint URL**. If your cluster does not have a public cloud service endpoint, [enable it](/docs/openshift?topic=openshift-cs_network_cluster#set-up-public-se).
        * Check that at least some of the worker nodes in your cluster have a **Public IP** address. If no worker node does, you must [set up public VLANs for at least one worker pool](/docs/openshift?topic=openshift-cs_network_cluster#change-vlans).
          ```
          ibmcloud oc workers -c <cluster_name_or_ID>
          ```
          {: pre}

4. In the output of Step 2, check that the **Ingress Subdomain** is available. The Ingress components in your cluster must provision before the router components can be created. If the **Ingress Subdomain** and **Ingress Secret** are not available, see [Why does no Ingress subdomain exist after cluster creation?](/docs/openshift?topic=openshift-ingress_subdomain).
5. Check that the **Hostname** of the router subdomain is in the format: `<cluster-name>-<accountID-hashed>-<ssll>.<region>.containers.appdomain.cloud`.
    ```
    ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
    ```
    {: pre}

    *  If the router subdomain is not updated after two hours of creating the cluster, review the **Master Status** of the cluster again, and follow any troubleshooting steps to resolve the issue.

If the troubleshooting steps do not resolve the issue, see [Getting help](/docs/openshift?topic=openshift-get-help).






