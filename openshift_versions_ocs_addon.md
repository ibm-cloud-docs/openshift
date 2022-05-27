---

copyright:
  years: 2014, 2022
lastupdated: "2022-05-27"

keywords: odf, openshift data foundation add-on, change log

subcollection: openshift, container storage

---

{{site.data.keyword.attribute-definition-list}}



# OpenShift Data Foundation add-on change log
{: #odf_addon_changelog}

View information for updates to the OpenShift Data Foundation add-on in your {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

Note that the add-on supports`n+1` cluster versions.
{: note}

To view a list of add-ons and the supported {{site.data.keyword.redhat_openshift_notm}} versions, see the [supported add-on versions table](/docs/openshift?topic=openshift-supported-cluster-addon-versions) or run the following command.

```sh
ibmcloud oc cluster addon versions --addon openshift-data-foundation
```
{: pre}

## Version 4.10
{: #4.10_odf}

### Version 4.10.2, released 23 May 2022
{: #4.10.2_odf}

Includes storage class encryption parameter parsing improvements.


### Version 4.10.1, released 20 May 2022
{: #4.10.1_odf}

- Includes support for {{site.data.keyword.hscrypto}} encryption.
- Updates the UBI to version `8.6-751`.

### Version 4.10.0, released 9 May 2022

Initial release.


## Version 4.9
{: #4.10_odf}

### Version 4.9.5, release 20 May 2022
{: #4.9.5_odf}

- Support update and scaling on {{site.data.keyword.satelliteshort}}.
- Golang update.
- Updates the UBI.

### Version 4.9.4, released 13 April 2022
{: #4.9.4_odf}

UBI update.

### Version 4.9.3, released 23 March 2022
{: #4.9.3_odf}

- Updates Golang.
- Updates the UBI.

### Version 4.9.2, released 24 February 2022
{: #4.9.2_odf}

Use PVC for mon on VPC.

### Version 4.9.1, released 23 Febraury 2022

Updates the UBI.

### Version 4.9.0, released 11 February 2022
{: #4.9.0_odf}

Initial release.


## Version 4.8
{: #4.8_odf}

### Version 4.8.4, release 17 January 2022
{: #4.8.4_odf}

Updates Golang version to 1.16.13.

### Version 4.8.3, released Jan 07, 2022
{: #4.8.3_odf}

- Updates UBI image.
- Adds increased logging.


### Version 4.8.2, released 03 January 2022
{: #4.8.2_odf}

- Removes MON parameters.
- Introduces local disk discovery.


### Version 4.8.1, released 17 November 2021
{: #4.8.1_odf}

- Removes {{site.data.keyword.satelliteshort}} link parameter.
- Updates Golang to 1.16.10.
- Updates the UBI.

### Version 4.8.0, released 25 October 2021
{: #4.8.0_odf}

Updates Golang to 1.16.9.

## Version 4.7
{: #4.7_odf}

### Version 4.7.14, released 25 October 2021
{: #4.7.14_odf}

Updateds Golang to 1.16.9.

### Version 4.7.13, released 13 October 2021
{: #4.7.13_odf}

Adds an agent health check.


### Version 4.7.12, released 30 September 2021
{: #4.7.12_odf}

Includes an NC check fix.

### Version 4.7.11, released 29 September 2021
{: #4.7.11_odf}

- Adds NC check.
- Updates the UBI.

### Version 4.7.10, released 15 September 2021
{: #4.7.10_odf}

Adds a fix for multiple operatorgroups. 


### Version 4.7.9, released 06 September 2021
{: #4.7.9_odf}

- Adds agent check
- Adds enhancements to cleanup.

### Version 4.7.8, released 16 August 202
{: #4.7.8_odf}

- Updates the UBI.
- Updates Golang to 1.16.7.

### Version 4.7.7, released 27 July 2021
{: #4.7.7_odf}

- Updates the UBI.
- Updates Golang to 1.16.6.

### Version 4.7.6, released 05 July 2021
{: #4.7.6_odf}

- Updates the UBI.
















