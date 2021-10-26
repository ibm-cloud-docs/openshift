---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-26"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why can't I establish VPN connectivity with the strongSwan Helm chart?
{: #cs_vpn_fails}

**Infrastructure provider**: ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic


When you check VPN connectivity by running `oc exec $STRONGSWAN_POD -- ipsec status`, you do not see a status of `ESTABLISHED`, or the VPN pod is in an `ERROR` state or continues to crash and restart.
{: tsSymptoms}


Your Helm chart configuration file has incorrect values, missing values, or syntax errors.
{: tsCauses}


To establish VPN connectivity with the strongSwan Helm chart, you might need to check for several types of issues and change your configuration file accordingly. To troubleshoot your strongSwan VPN connectivity:
{: tsResolve}

1. [Test and verify the strongSwan VPN connectivity](/docs/openshift?topic=openshift-vpn#vpn_test) by running the five Helm tests that are included in the strongSwan chart definition.

2. If you are unable to establish VPN connectivity after running the Helm tests, you can run the VPN debugging tool that is packaged inside of the VPN pod image.

    1. Set the `STRONGSWAN_POD` environment variable.
        ```sh
        export STRONGSWAN_POD=$(oc get pod -l app=strongswan,release=vpn -o jsonpath='{ .items[0].metadata.name }')
        ```
        {: pre}

    2. Run the debugging tool.
        ```sh
        oc exec $STRONGSWAN_POD -- vpnDebug
        ```
        {: pre}

        The tool outputs several pages of information as it runs various tests for common networking issues. Output lines that begin with `ERROR`, `WARNING`, `VERIFY`, or `CHECK` indicate possible errors with the VPN connectivity.




