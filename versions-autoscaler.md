---

copyright: 
  years: 2014, 2022
lastupdated: "2022-05-06"

keywords: autoscaler, add-on, autoscaler changelog, cluster autoscaler, scale

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Cluster autoscaler add-on changelog
{: #ca_changelog}

View information for patch updates to the cluster autoscaler add-on in your {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

Patch updates
:   Patch updates are delivered automatically by IBM and don't contain any feature updates or changes in the supported add-on and cluster versions.

Release updates
:   Release updates contain new features for the cluster autoscaler or changes in the supported add-on or cluster versions. You must manually apply release updates to your cluster autoscaler add-on. To update your cluster autoscaler add-on, see [Updating the cluster autoscaler add-on](/docs/openshift?topic=openshift-cluster-scaling-install-addon#cluster-scaling-update-addon).

Refer to the following tables for a summary of changes for each version of the [cluster autoscaler add-on](/docs/containers?topic=containers-cluster-scaling-classic-vpc).

As of 23 June 2021, version `1.0.2` of the cluster autoscaler add-on is deprecated and becomes unsupported on 23 July 2021. Version `1.0.3`, which adds support for Kubernetes 1.21 is now available. If you have a deprecated or unsupported version of the add-on installed in your cluster, update the add-on to version `1.0.3`. To update the add-on in your cluster, disable the add-on and then re-enable the add-on. You might see a warning that resources or data might be deleted. For the cluster autoscaler update, any autoscaling operations that are in process when you disable the add-on fail. When you re-enable the add-on, autoscaling operations are restarted for you. Existing cluster autoscaler resources like the `iks-ca-configmap` are retained even after you disable the add-on. Your worker nodes are not deleted because of disabling the add-on.
{: important}

To view a list of add-ons and the supported cluster versions, run the following command.
```sh
ibmcloud oc cluster addon versions --addon cluster-autoscaler
```
{: pre}

| Cluster autoscaler add-on version | Supported? | Cluster version support |
| -------------------- | -----------|--------------------------- |
| 1.1.0 | Yes |  >=4.6 |
| 1.0.5 | Yes |  >=4.3 |
| 1.0.4 | Yes |  >=4.3 |
| 1.0.3 | Yes |  >=4.3 |
| 1.0.2 | Yes |  4.3 - 4.6 |
| 1.0.1 | No |  4.3 - 4.6 |
{: summary="The rows are read from left to right. The first column is the cluster autoscaler add-on version. The second column is the version's supported state. The third column is the cluster version of your cluster that the cluster autoscaler version is supported for."}

## Version 1.1.0
{: #0110_ca_addon}

Review the changes included in version 1.1.0 of the managed cluster autoscaler add-on.
{: shortdesc}

### Change log for patch update 1.1.0_475, released 30 March 2022
{: #110475_ca}

- Image tags: `1.19.1-12`, `1.20.0-12`, `1.21.0-8`, `1.22.0-6`, `1.23.0-3`
- Resolves [CVE-2022-24921](https://nvd.nist.gov/vuln/detail/CVE-2022-24921{: external}.
- Adds permissions for `cluster-autoscaler` to watch namespaces.

### Change log for patch update 1.1.0_429, released 16 March 2022
{: #110429_ca}

- Image tags: `1.19.1-11`, `1.20.0-11`, `1.21.0-7`, `1.22.0-5`, `1.23.0-2`
- Adds Beta support for {{site.data.keyword.satelliteshort}} clusters in allowlisted accounts.

## Version 1.0.5
{: #0105_ca_addon}

Review the changes included in version 1.0.5 of the managed cluster autoscaler add-on.
{: shortdesc}

### Change log for patch update 1.0.5_415, released 28 February 2022
{: #104415_ca}

Image tags: `1.19.1 9`, `1.20.0 9`, `1.21.0 5`, `1.22.0 3`
Adds support for Kubernetes 1.23


## Version 1.0.4
{: #0104_ca_addon}

Review the changes included in version 1.0.4 of the managed cluster autoscaler add-on.
{: shortdesc}


### Change log for patch update 1.0.4_410, released 23 February 2022
{: #104410_ca}

Image tags: `1.19.1 9`, `1.20.0 9`, `1.21.0 5`, `1.22.0 3`
Resolves the following CVEs: [CVE-2022-23772](https://nvd.nist.gov/vuln/detail/CVE-2022-23772){: external}, [CVE-2022-23773](https://nvd.nist.gov/vuln/detail/CVE-2022-23773){: external}, and [CVE-2022-23806](https://nvd.nist.gov/vuln/detail/CVE-2022-23806){: external}.




### Change log for patch update 1.0.4_403, released 20 January 2022
{: #104403_ca}

Review the changes in version `1.0.4_403` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.19.1-8`, `1.20.0-8`, `1.21.0-4`, and `1.22.0-2`.
- Supported cluster versions: 4.3
- Includes fixes for [CVE-2021-44716](https://nvd.nist.gov/vuln/detail/CVE-2021-44716{: external} and [CVE-2021-44717](https://nvd.nist.gov/vuln/detail/CVE-2021-44717){: external}. 


### Change log for patch update 1.0.4_387, released 22 November 2021
{: #104387_ca}

Review the changes in version `1.0.4_387` of the cluster autoscaler add-on. 
{: shortdesc}

- Image tags: `1.19.1-7`, `1.20.0-7`, `1.21.0-3`, and `1.22.0-2`.
- Updates the Golang version to `1.16.10` which includes fixes for [CVE-2021-41772](https://nvd.nist.gov/vuln/detail/CVE-2021-41772){: external} and [CVE-2021-41771](https://nvd.nist.gov/vuln/detail/CVE-2021-41771){: external}.

### Change log for patch update 1.0.4_374, released 7 October 2021
{: #104374_ca}

Review the changes in version `1.0.4_374` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.19.1-6`, `1.20.0-6`, `1.21.0-2`, and `1.22.0-1`.
- Adds support for Kubernetes version 1.22
- Pulls the base Golang image from a proxy registry.
- Adds an owner label to the `cluster-autoscaler` images.




## Version 1.0.3
{: #0103_ca_addon}

Review the changes included in version 1.0.3 of the managed cluster autoscaler add-on.
{: shortdesc}



### Change log for patch update 1.0.3_360, released 26 August 2021
{: #103360_ca}

Review the changes in version `1.0.3_360` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags:  `1.17.4-5`, `1.18.3-5`, `1.19.1-5`, `1.20.0-5`, and `1.21.0-1`.  
- Supported cluster versions: >=4.3  
- Updates the Golang version to `1.16.6` which includes a fix for `PVR0281096`.  
- Increases the default resource requests and limits.
    - Previous values:
        ```yaml
        resourcesLimitsCPU: "600m"	    
        resourcesLimitsMemory: "600Mi"	     
        resourcesRequestsCPU: "200m"	      
        resourcesRequestsMemory: "200Mi"
        ```
        {: screen}	

    - Updated values:
        ```yaml
        resourcesLimitsCPU: "800m"
        resourcesLimitsMemory: "1000Mi"
        resourcesRequestsCPU: "200m"
        resourcesRequestsMemory: "400Mi"
        ```
        {: screen}




### Change log for patch update 1.0.3_352, released 23 June 2021
{: #103352_ca}

Review the changes in version `1.0.3_352` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.17.4-4`, `1.18.3-4`, `1.19.1-4`, `1.20.0-4`, and `1.21.0-0`.   
- Supported cluster versions: >=4.3  
- Adds support for Kubernetes 1.21.  



## Version 1.0.2
{: #0102_ca_addon}

Review the changes that are in version 1.0.2 of the managed cluster autoscaler add-on.
{: shortdesc}



### Change log for patch update 1.0.2_267, released 10 May 2021
{: #102267_ca}

Review the changes in version `1.0.2_267` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.17.4-3`, `1.18.3-3`, `1.19.1-3`, and `1.20.0-3`.  
- Supported cluster versions: 4.3 - 4.6  
- Includes a bug fix for the `worker replace` command on VPC clusters that caused worker creation to fail.  

### Change log for patch update 1.0.2_256, released 19 April 2021 
{: #102256_ca}

Review the changes in version `1.0.2_256` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.17.4-2`, `1.18.3-2`, `1.19.1-2`, and `1.20.0-2`  
- Supported cluster versions: 4.3 - 4.6  
- Includes fixes for [CVE-2021-27919](https://nvd.nist.gov/vuln/detail/CVE-2021-27919){: external} and [CVE-2021-27918](https://nvd.nist.gov/vuln/detail/CVE-2021-27918){: external}.  

### Change log for patch update 1.0.2_249, released 01 April 2021
{: #102249_ca}

Review the changes in version `1.0.2_249` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.16.7-1`, `1.17.4-1`, `1.18.3-1`, `1.19.1-1`, and `1.20.0-1`.  
- Supported cluster versions: 4.3 - 4.6  
- Includes fixes for [CVE-2021-3114](https://nvd.nist.gov/vuln/detail/CVE-2021-3114){: external} and [CVE-2021-3115](https://nvd.nist.gov/vuln/detail/CVE-2021-3114){: external}.  
- Removes the `init` container. In previous versions, the cluster autoscaler pods would remain in the `initContainer` state if the API key was missing or malformed. This update removes the `init` container so that if the API key is missing or malformed, the cluster autoscaler pod fails.  

### Change log for patch update 1.0.2_224, released 09 March 2021
{: #10224_ca}

Review the changes in version `1.0.2_224` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.16.7-0`, `1.17.4-0`, `1.18.3-0`, `1.19.1-0`, and `1.20.0-0`.  
- Supported cluster versions: 4.3 - 4.6  
- Adds support for Kubernetes version 1.20.  


## Version 1.0.1
{: #0101_ca_addon}

Review the changes that are in version 1.0.1 of the managed cluster autoscaler add-on.  
{: shortdesc}



### Change log for patch update 1.0.1_219, released 16 February 2021
{: #101219_ca}

Review the changes in version `1.0.1_219` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.16.7-0` `1.17.4-0`, `1.18.3-0`, and `1.19.1-0`.  
- Supported cluster versions: 4.3 - 4.6  
- Updates the code base to synchronize with the community autoscaler. For more information, see the [Kubernetes autoscaler documentation](https://github.com/kubernetes/autoscaler/releases){: external}.  

### Change log for patch update 1.0.1_210, released 13 January 2021
{: #101210_ca}

Review the changes in version `1.0.1_210` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.16.2-9`, `1.17.0-10`, `1.18.1-9`, and `1.19.0-4`.  
- Supported cluster versions: 4.3 - 4.6  
- Update addresses [`DLA-2509-1`](https://www.debian.org/lts/security/2020/dla-2509){: external}.  

### Change log for patch update 1.0.1_205, released 15 December 2020
{: #101205_ca}

Review the changes in version `1.0.1_205` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.11.0-7`, `1.16.2-8`, `1.17.0-9`, `1.18.1-8`, and `1.19.0-3`.  
- Supported cluster versions: 4.3 - 4.6  
- Updates the `initContainer` to use the universal base image (UBI).  

### Change log for patch update 1.0.1_195, released 10 December 2020
{: #101195_ca}

Review the changes in version `1.0.1_195` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.11.0-7`, `1.16.2-8`, `1.17.0-9`, `1.18.1-8`, and `1.19.0-3`.  
- Supported cluster versions: 4.3 - 4.6  
- Images are now signed.  
- Resources that are deployed by the cluster autoscaler add-on are now linked with the corresponding source code and build URLs.  
- Updates the Go version to `1.15.5`.  

### Change log for patch update 1.0.1_146, released 03 December 2020
{: #101146_ca}

Review the changes in version `1.0.1_146` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.15.4-4`, `1.16.2-7`, `1.17.0-8`, `1.18.1-7`, and `1.19.0-2`.  
- Supported cluster versions: 4.3 - 4.6  
- Updates the cluster autoscaler to run as non-root.  
- Adds a feature to validate secrets before the autoscaler pods are initialized.  

### Change log for patch update 1.0.1_128, released 27 October 2020
{: #101128_ca}

Review the changes in version `1.0.1_128` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.15.4-4`, `1.16.2-6`, `1.17.0-7`, `1.18.1-6`, and `1.19.0-1`.  
- Supported cluster versions: 4.3 - 4.5  
- Updates the Go version to `1.15.2`.  

### Change log for patch update 1.0.1_124, released 16 October 2020
{: #101124_ca}

Review the changes in version `1.0.1_124` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.15.4-4`, `1.16.2-6`, `1.17.0-7`, `1.18.1-6`, and `1.19.0-1`.  
- Supported cluster versions: 4.3 - 4.5  
- Exposes the `--new-pod-scale-up-delay` flag in the configmap.  
- Adds support for Kubernetes 1.19.  

### Change log for patch update 1.0.1_114, released 10 September 2020
{: #101114_ca}

Review the changes in version `1.0.1_114` of the cluster autoscaler add-on.
{: shortdesc}

- Image tags: `1.15.4-4`, `1.16.2-5`, `1.17.0-6`, and `1.18.1-5`.  
- Supported cluster versions: 4.3 - 4.5  
- Includes fixes for `CVE-5188` and `CVE-3180`.  
- Unlike the previous Helm chart, you can modify all the add-on configuration settings via a single configmap.  

