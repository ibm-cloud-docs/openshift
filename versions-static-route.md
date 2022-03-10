---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-10"

keywords: openshift, static route, add-on

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Static route add-on version changelog
{: #static-route-changelog}

For deployment steps, see the [managed static route add-on](/docs/containers?topic=containers-static-routes) docs.
{: shortdesc}

For steps on updating the static route add-on, see [Updating managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

Review the supported versions of the static route add-on. In the CLI, you can run `ibmcloud oc cluster addon versions --addon static-route`.

| Static route add-on version | Supported? | {{site.data.keyword.redhat_openshift_notm}} version support |
| --- | --- | --- |
| 1.00 | Yes | 4.5, 4.6, 4.7 |
{: summary="The rows are read from left to right. The first column is the static route add-on version. The second column is the version's supported state. The third column is the {{site.data.keyword.redhat_openshift_notm}} version of your cluster that the static route add-on version is supported for."}
{: caption="Supported static route add-on versions" caption-side="top"}

## Version 1.0.0
{: #v100}

### Changelog for 1.0.0_649, released 8 September 2021
{: #100_649}

**Previous version:** 1.0.0_572 **Current version:** 1.0.0_649
**Updates in this version:**
- Uses `apiextensions.k8s.io/v1` instead of `apiextensions.k8s.io/v1beta1`.




