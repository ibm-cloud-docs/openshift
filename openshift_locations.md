---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: openshift, roks, rhoks, rhos, mzr, szr, multizone, multi az

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Locations
{: #regions-and-zones}

You can deploy {{site.data.keyword.openshiftlong}} clusters worldwide. When you create a cluster, its resources remain in the location that you deploy the cluster to. To work with your cluster, you can access the OpenShift Service via a global API endpoint.
{:shortdesc}



## Red Hat OpenShift on IBM Cloud locations
{: #locations}

{{site.data.keyword.cloud_notm}} resources are organized into a hierarchy of geographic locations. Red Hat OpenShift on IBM Cloud is available in a subset of these locations. Other {{site.data.keyword.cloud_notm}} services might be available globally or within a specific location.
{: shortdesc}

### Available locations
{: #available-locations}

To list available Red Hat OpenShift on IBM Cloud locations, use the `ibmcloud oc supported-locations` command.
{: shortdesc}

The following image is used as an example to explain how Red Hat OpenShift on IBM Cloud locations are organized.

![Organization of Red Hat OpenShift on IBM Cloud locations](images/cs_regions_hierarchy.png)

<table summary="The table shows organization of Red Hat OpenShift on IBM Cloud locations. Rows are to be read from the left to right, with the location type in column one, an example of the type in column two, and the description in column three.">
<caption>Organization of Red Hat OpenShift on IBM Cloud locations.</caption>
  <thead>
  <th>Type</th>
  <th>Example</th>
  <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td>Geography</td>
      <td>North America (`na`)</td>
      <td>An organizational grouping that is based on geographic continents.</td>
    </tr>
    <tr>
      <td>Country</td>
      <td>Canada (`ca`)</td>
      <td>The location's country within the geography.</td>
    </tr>
    <tr>
      <td>Metro</td>
      <td>Mexico City (`mex-cty`), Dallas (`dal`)</td>
      <td>The name of a city where 1 or more data centers (zones) are located. A metro can be multizone-capable and have multizone-capable data centers, such as Dallas, or can have only single zone data centers, such as Mexico City. If you create a cluster in a multizone-capable metro, the Kubernetes master and worker nodes can be spread across zones for high availability.</td>
    </tr>
    <tr>
      <td>Data center (zone)</td>
      <td>Dallas 12 (`dal12`)</td>
      <td>A physical location of the compute, network, and storage infrastructure and related cooling and power that host cloud services and applications. Clusters can be spread across data centers, or zones, in an multizone architecture for high availability. Zones are isolated from each other, which ensures no shared single point of failure.</td>
    </tr>
  </tbody>
  </table>

### Multizone locations in Red Hat OpenShift on IBM Cloud
{: #zones}

The following tables list the available multizone locations in Red Hat OpenShift on IBM Cloud. You can choose to create clusters with worker nodes in one zone of the multizone metro, or spread the workers across all three zones within each metro to protect your apps from a zone failure. Whether you create the workers in a single zone or across zones, the replicas of your highly available master are automatically spread across zones.
{: shortdesc}

To quickly determine whether a zone is multizone-capable, your can run `ibmcloud oc supported-locations` and look for the value in the `Multizone Metro` column.
{: tip}

{{site.data.keyword.cloud_notm}} resources used to be organized into regions that were accessed via [region-specific endpoints](#bluemix_regions). The tables list the previous regions for informational purposes. Going forward, you can use the [global endpoint](#endpoint) to move toward a region-less architecture.
{: deprecated}

**Multizone metro locations**

<table summary="The table shows the available multizone metro locations in Red Hat OpenShift on IBM Cloud. Rows are to be read from the left to right.  Column one is the geography that the location is in, column two is the country of the location, column three is the metro of the location, column four is the data center, and column five is the deprecated region that the location used to be organized into.">
<caption>Available multizone metro locations in Red Hat OpenShift on IBM Cloud.</caption>
  <thead>
  <th>Geography</th>
  <th>Country</th>
  <th>Metro</th>
  <th>Data center</th>
  <th>Deprecated region</th>
  </thead>
  <tbody>
    <tr>
      <td>Europe</td>
      <td>United Kingdom</td>
      <td>London</td>
      <td>lon04, lon05, lon06</td>
      <td>UK South (`uk-south`, `eu-gb`)</td>
    </tr>
    <tr>
      <td>North America</td>
      <td>United States</td>
      <td>Washington, D.C.</td>
      <td>wdc04, wdc06, wdc07</td>
      <td>US East (`us-east`)</td>
    </tr>
  </tbody>
  </table>

### Multizone clusters
{: #regions_multizone}

In a multizone cluster, your cluster's resources are spread across multiple zones for higher availability.
{: shortdesc}

1.  Worker nodes are spread across multiple zones in the metro location to provide more availability for your cluster. The Kubernetes master replicas are also spread across zones. When you initiate local container orchestration actions, such as `oc` commands, the information is exchanged between your master and worker nodes through the global endpoint.

2.  Other cluster resources, such as storage, networking, compute, or apps running in pods, vary in how they deploy to the zones in your multizone cluster. For more information, review these topics:
    *   Setting up [file storage](/docs/openshift?topic=openshift-file_storage#add_file) and [block storage](/docs/openshift?topic=openshift-block_storage#add_block) in multizone clusters, or [choosing a multizone persistent storage solution](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).
    *   [Enabling public or private access to an app by using a network load balancer (NLB) service in a multizone cluster](/docs/containers?topic=containers-loadbalancer#multi_zone_config).
    *   [Managing network traffic by using Ingress](/docs/containers?topic=containers-ingress-about).
    *   [Increasing the availability of your app](/docs/containers?topic=containers-app#increase_availability).

3.  When you initiate cluster management actions, such as using [`ibmcloud oc` commands](/docs/openshift?topic=openshift-cli-plugin-kubernetes-service-cli), basic information about the cluster (such as name, ID, user, the command) is routed through the global endpoint.

<br />


## Accessing the global endpoint
{: #endpoint}

You can organize your resources across {{site.data.keyword.cloud_notm}} services by using {{site.data.keyword.cloud_notm}} locations (formerly called regions). For example, you can create an OpenShift cluster by using a private Docker image that is stored in your {{site.data.keyword.registryshort_notm}} of the same location. To access these resources, you can use the global endpoints and filter by location.
{:shortdesc}

### Logging in to {{site.data.keyword.cloud_notm}}
{: #login-ic}

When you log in to the {{site.data.keyword.cloud_notm}} (`ibmcloud`) command line, you are prompted to select a region. However, this region does not affect the Red Hat OpenShift on IBM Cloud plug-in (`ibmcloud oc`) endpoint, which still uses the global endpoint. Note that you do still need to target the resource group that your cluster is in if it is not in the default resource group.
{: shortdesc}

To log in to the {{site.data.keyword.cloud_notm}} global API endpoint and target the resource group that your cluster is in:
```
ibmcloud login -a https://cloud.ibm.com -g <nondefault_resource_group_name>
```
{: pre}

### Logging in to Red Hat OpenShift on IBM Cloud
{: #login-iks}

When you log in to {{site.data.keyword.cloud_notm}}, you can access the {{site.data.keyword.containershort_notm}}. To help you get started, check out the following resources for using the Red Hat OpenShift on IBM Cloud CLI and API.
{: shortdesc}

**Red Hat OpenShift on IBM Cloud CLI**:

[Set up your CLI to use the `ibmcloud oc` plug-in](/docs/openshift?topic=openshift-cs_cli_install#cs_cli_install). By default, you are logged in to the global Red Hat OpenShift on IBM Cloud endpoint, `https://containers.cloud.ibm.com`.

When you use the new global functionality in the Red Hat OpenShift on IBM Cloud CLI, consider the following changes from the legacy region-based functionality.

* Listing resources:
  * When you list resources, such as with the `ibmcloud oc clusters`, `ibmcloud oc subnets`, or `ibmcloud oc zones` commands, resources in all locations are returned. To filter resources by a specific location, certain commands include a `--locations` flag. For example, if you filter clusters for the `wdc` metro, multizone clusters in that metro and single-zone clusters in data centers (zones) within that metro are returned. If you filter clusters for the `wdc06` data center (zone), multizone clusters that have a worker node in that zone and single-zone clusters in that zone are returned. Note that you can pass one location or a comma-separated list of locations.
    Example to filter by location:
    ```
    ibmcloud oc clusters --locations dal
    ```
    {: pre}
  * Other commands do not return resources in all locations. To run `credential-set/unset/get`, `api-key-reset`, and `vlan-spanning-get` commands, you must specify a region in the `--region`.

* Working with resources:
  * When you use the global endpoint, you can work with resources that you have access permissions to in any location, even if you set a region by running `ibmcloud oc region-set` and the resource that you want to work with is in another region.
  * If you have clusters with the same name in different regions, you can either use the cluster ID when you run commands or set a region with the `ibmcloud oc region-set` command and use the cluster name when you run commands.

* Legacy functionality:
  * If you need to list and work with resources from one region only, you can use the `ibmcloud oc init` [command](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_init) to target a regional endpoint instead of the global endpoint.
    Example to target the US South regional endpoint:
    ```
    ibmcloud oc init --host https://us-south.containers.cloud.ibm.com
    ```
    {: pre}
  * To use the global functionality, you can use the `ibmcloud oc init` command again to target the global endpoint. Example to target the global endpoint again:
    ```
    ibmcloud oc init --host https://containers.cloud.ibm.com
    ```
    {: pre}

</br></br>
**Red Hat OpenShift on IBM Cloud API**:
* [Get started with the API](/docs/containers?topic=containers-cs_cli_install#cs_api).
* [View documentation on the API commands](https://containers.cloud.ibm.com/global/swagger-global-api/).
* Generate a client of the API to use in automation by using the [`swagger.json` API](https://containers.cloud.ibm.com/global/swagger-global-api/swagger.json).

To interact with the global Red Hat OpenShift on IBM Cloud API, enter the command type and append `global/v1/command` to the endpoint.

Example of `GET /clusters` global API:
```
GET https://containers.cloud.ibm.com/global/v1/clusters
```
{: codeblock}

</br>

If you need to specify a region in an API call, remove the `/global` parameter from the path and pass the region name in the `X-Region` header. To list available regions, run `ibmcloud oc regions`.

<br />

