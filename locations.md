---

copyright: 
  years: 2014, 2024
lastupdated: "2024-09-23"


keywords: openshift, mzr, szr, multizone, multi az

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Locations
{: #regions-and-zones}

[{{site.data.keyword.cloud_notm}} resources](/docs/overview?topic=overview-locations) are organized into a hierarchy of geographic locations. {{site.data.keyword.openshiftlong_notm}} is available in a subset of the {{site.data.keyword.cloud_notm}} locations, including worldwide multizone regions (MZRs) and single-campus multizone regions (SC-MZRs).
{: shortdesc}

![{{site.data.keyword.openshiftlong_notm}} locations](images/locations.svg){: caption="Figure 1. {{site.data.keyword.openshiftlong_notm}} locations" caption-side="bottom"}

This image is an artistic representation and does not reflect actual political or geographic boundaries.
{: note}


## {{site.data.keyword.openshiftlong_notm}} locations
{: #locations}

You can deploy {{site.data.keyword.openshiftlong}} clusters worldwide. When you create a cluster, its resources remain in the location that you deploy the cluster to. To work with your cluster, you can access the service via a global API endpoint.
{: shortdesc}


### Classic regions with multiple data centers
{: #zones-mz}

If you create a classic cluster with multiple data centers, the replicas of your highly available Kubernetes master are automatically spread across the data centers. You have the option to spread your worker nodes across zones to protect your apps from a zone failure. To determine whether a location has a multizone region, your can run `ibmcloud oc locations` and look for the value in the `Multizone Metro` column.
{: shortdesc}

| Geography | Country | Metro | Region | Zones |
| --- | --- | --- | --- | --- |
| Asia Pacific | Australia | Sydney | au-syd | syd01, syd04, syd05 |
| Asia Pacific | Japan | Osaka | jp-osa | osa21, osa22, osa23 |
| Asia Pacific | Japan | Tokyo | jp-tok | tok02, tok04, tok05 |
| Europe | Germany | Frankfurt | de-fra | fra02, fra04, fra05 |
| Europe | United Kingdom | London | uk-lon | lon02, lon04, lon05, lon06 |
| North America | United States | Dallas | us-dal | dal10, dal12, dal13 |
| North America | United States | Washington DC | us-wdc | wdc04, wdc06, wdc07 |
{: caption="Available multizone regions for classic clusters in {{site.data.keyword.openshiftlong_notm}}." caption-side="bottom"}
{: #classic-multizone-locations-table}





### Classic regions with one data center
{: #zones-sz}

If you create a classic cluster in a region with only one data center, the highly available master includes three replicas on separate hosts, but is not spread across zones.
{: shortdesc}

Classic single zone clusters are managed from the regional endpoint located in the nearest region that supports classic multizone, such as `mon01` to `us-east` or `sao01` to `us-south`.

| Geography | Country | Metro | Region | Zone | Managed from region |
| --- | --- | --- | --- | --- | --- |
| Asia Pacific | India | Chennai | in-che | che01 | AP North (`ap-north`, `jp-tok`) |
| Asia Pacific | Singapore | Singapore | sng-mtr | sng01 | AP North (`ap-north`, `jp-tok`) |
| Europe | France | Paris | fr-par | par01 | EU Central (`eu-central`, `eu-de`) |
| Europe | Italy | Milan | it-mil | mil01 | EU Central (`eu-central`, `eu-de`) |
| Europe | Netherlands | Amsterdam | nl-ams | ams03 | EU Central (`eu-central`, `eu-de`) |
| North America | Canada | Montreal | ca-mon | mon01 | US East (`us-east`) |
| North America | Canada | Toronto | ca-tor | tor01 | US East (`us-east`) |
| North America | United States | San Jose | us-sjc | sjc03, sjc04 | US South (`us-south`) |
| South America | Brazil | Sao Paulo | br-sao | sao01 | US South (`us-south`) |
{: caption="Available single zone data centers for classic clusters in {{site.data.keyword.openshiftlong_notm}}." caption-side="bottom"}
{: #classic-single-zone-locations-table}



### VPC multizone regions
{: #zones-vpc}

VPC resources are provisioned in a region, which is a separate group of zones within a metro. The zones are mapped to separate data centers to ensure that resources are distributed evenly across zones in a multizone architecture. In the API and CLI, zones use the regional zone name in the API and command line (`us-south-1`), but in the console, zones use by the data center location (`Dallas 1`). For the data center code that the VPC zone and location corresponds to, such as `us-south-1` and `DAL10`, see [Multizone regions](/docs/overview?topic=overview-locations#table-mzr).
{: shortdesc}

| Geography | Country | Metro | Region | Zones |
| --- | --- | --- | --- | --- |
| Asia Pacific | Australia | Sydney | au-syd | au-syd-1, au-syd-2, au-syd-3 |
| Asia Pacific | Japan | Osaka | jp-osa | jp-osa-1, jp-osa-2, jp-osa-3 |
| Asia Pacific | Japan | Tokyo | jp-tok | jp-tok-1, jp-tok-2, jp-tok-3 |
| Europe | Germany | Frankfurt | eu-de | eu-de-1, eu-de-2, eu-de-3 |
| Europe | Spain | `†` Madrid | eu-es | eu-es-1, eu-es-2, eu-es-3 |
| Europe | United Kingdom | London | eu-gb | eu-gb-1, eu-gb-2, eu-gb-3 |
| North America | Canada | `†` Toronto | ca-tor | ca-tor-1, ca-tor-2, ca-tor-3 |
| North America | United States | Dallas | us-south | us-south-1, us-south-2, us-south-3 |
| North America | United States | Washington DC | us-east | us-east-1, us-east-2, us-east-3 |
| South America | Brazil | `†` São Paulo | br-sao | br-sao-1, br-sao-2, br-sao-3 |
{: caption="Available multizone regions for VPC clusters in {{site.data.keyword.openshiftlong_notm}}." caption-side="bottom"}
{: #vpc-gen2-multizone-locations-table}



`†` These regions are available as multizone regions for clusters on VPC infrastructure only.



### {{site.data.keyword.satelliteshort}} regions
{: #sat-regions-openshift}

To see a list of the supported `Managed from` regions for {{site.data.keyword.satelliteshort}} clusters, [Supported {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-sat-regions).



## Where are the resources?
{: #regions_resources}

### Resources in a single zone cluster
{: #regions_single_zone}

In a single zone cluster, your cluster's resources remain in the data center (zone) in which the cluster is deployed, but management operations might be routed through a regional endpoint.
{: shortdesc}

Your cluster's resources, including the master and worker nodes, are in the same zone that you deployed the cluster to. When you initiate local container orchestration actions, such as `oc` commands, the information is exchanged between your master and worker nodes within the same zone.

If you set up other cluster resources, such as storage, networking, compute, or apps running in pods, the resources and their data remain in the zone that you deployed your cluster to.

When you initiate cluster management actions, such as running **`ibmcloud oc`** commands, basic information about the cluster such as name, ID, user, the command is routed through a regional endpoint and the global endpoint. 



### Resources in a multizone cluster
{: #regions_multizone}

In a multizone cluster, your cluster's resources are spread across multiple zones for higher availability.
{: shortdesc}

Worker nodes are spread across multiple zones in the region to provide more availability for your cluster. The Kubernetes master replicas are also spread across zones. When you initiate local container orchestration actions, such as **`oc`** commands, the information is exchanged between your master and worker nodes through the global endpoint.

Other cluster resources, such as storage, networking, compute, or apps running in pods, vary in how they deploy to the zones in your multizone cluster. For more information, review these topics:
*   Setting up [file storage](/docs/openshift?topic=openshift-file_storage#add_file) and [block storage](/docs/openshift?topic=openshift-block_storage#add_block) in multizone clusters, or [choosing a multizone persistent storage solution](/docs/openshift?topic=openshift-storage-plan).
*   [Enabling public or private access to an app by using a network load balancer (NLB) service in a multizone cluster](/docs/openshift?topic=openshift-loadbalancer#multi_zone_config).
*   [Managing network traffic by using Ingress](/docs/containers?topic=containers-managed-ingress-about).
*   [Increasing the availability of your app](/docs/openshift?topic=openshift-app).

When you initiate cluster management actions, such as running [`ibmcloud oc` commands](/docs/openshift?topic=openshift-kubernetes-service-cli), basic information about the cluster, such as name, ID, user, the command is routed through the global endpoint.



## Accessing resources
{: #endpoint}

You can organize your resources across {{site.data.keyword.cloud_notm}} services by using {{site.data.keyword.cloud_notm}} locations (or regions). For example, you can deploy an app to a cluster by using a private Docker image that is stored in your {{site.data.keyword.registrylong_notm}} of the same location. To access these resources, you can use the global endpoints and filter by location.
{: shortdesc}

### Accessing resources from the CLI
{: #endpoint_cli}

1. [Install the CLI](/docs/openshift?topic=openshift-cli-install).

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

    When you log in to the {{site.data.keyword.cloud_notm}} (`ibmcloud`) command line, you are prompted to select a region. However, this region does not affect the {{site.data.keyword.openshiftlong_notm}} plug-in (`ibmcloud oc`) endpoint, which still uses the global endpoint. Note that you do still need to target the resource group that your cluster is in if it is not in the default resource group.

1. [Review the CLI commands](/docs/containers?topic=containers-kubernetes-service-cli). 

    * Listing resources:
        * When you list resources, such as with the `ibmcloud oc cluster ls`, `ibmcloud oc subnets`, or `ibmcloud oc zone ls` commands, resources in all locations are returned. To filter resources by a specific location, certain commands include a `--location` option. For example, if you filter clusters for the `wdc` metro, multizone clusters in that metro and single-zone clusters in data centers (zones) within that metro are returned. If you filter clusters for the `wdc06` data center (zone), multizone clusters that have a worker node in that zone and single-zone clusters in that zone are returned. `ibmcloud oc cluster ls -l dal`.

        * Other commands don't return resources in all locations. To run `credential set/unset/get`, `api-key reset`, and `vlan spanning get` commands, you must specify a region in the `--region`.

    * Working with resources:
        * When you use the global endpoint, you can work with resources that you have access permissions to in any location, even if you target one region and the resource that you want to work with is in another region.
        * If you have clusters with the same name in different regions, use the cluster ID when you run commands or set a region with the `ibmcloud oc init` command and use the cluster name when you run commands.


### Accessing resources from the API
{: #endpoint_api}

1. [Get started with the API](/docs/openshift?topic=openshift-cs_api_install#cs_api).

1. [Review the API commands](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external}.

    To interact with the global {{site.data.keyword.openshiftlong_notm}} API, enter the command type and append `global/v1/command` to the endpoint.

    Example of `GET /clusters` global API:
    ```sh
    GET https://containers.cloud.ibm.com/global/v1/clusters
    ```
    {: codeblock}

    If you need to specify a region in an API call, remove the `/global` parameter from the path and pass the region name in the `X-Region` header. To list available regions, review the [Previous region](#zones-mz) column in the {{site.data.keyword.openshiftlong_notm}} locations table.

1. Optional: Generate a client of the API to use in automation by using the [`swagger.json` API](https://containers.cloud.ibm.com/global/swagger-global-api/swagger.json){: external}.
