---

copyright: 
  years: 2014, 2024
lastupdated: "2024-10-02"


keywords: openshift, static route, add-on

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Static route add-on change log
{: #versions-static-route}

For deployment steps, see the [managed static route add-on](/docs/openshift?topic=openshift-static-routes) docs.
{: shortdesc}

For steps on updating the static route add-on, see [Updating managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

To view a list of add-ons and the supported cluster versions, run the following command or see the [Supported cluster add-ons table](/docs/openshift?topic=openshift-supported-cluster-addon-versions).

```sh
ibmcloud oc cluster addon versions
```
{: pre}


## Version 1.0.0
{: #v100}

### Change log for 1.0.0_1415, released 3 October 2024
{: #100_1415}

- Updates the Operator SDK version to `1.36.1`.
- Updates the Go builder version to `1.22`.
- Fixes a bug in `nodeSelector` that did not properly select nodes on a multi-subnet cluster.


### Change log for 1.0.0_1122, released 17 July 2023
{: #100_1122}

Adds support for multiple worker node architectures.



### Change log for 1.0.0_649, released 8 September 2021
{: #100_649}

- Uses `apiextensions.k8s.io/v1` instead of `apiextensions.k8s.io/v1beta1`.
