---

copyright: 
  years: 2014, 2025
lastupdated: "2025-04-29"


keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}





# Checking the status of Ingress components
{: #ingress-status}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

## Getting the status and message
{: #check_status}

To check the overall health and status of your cluster's Ingress components:
{: shortdesc}

```sh
ibmcloud oc ingress status-report get -c <cluster_name_or_ID>
```
{: pre}

The state of the Ingress components are reported in an **Ingress Status** and **Ingress Message**.

Example output




```sh
Ingress Status:   healthy
Message:          All Ingress components are healthy.

Cluster            Status
ingress-operator   healthy
route-admission    healthy

Subdomain                                                                           Status
example-ae7743ca70a399d9cff4eaf617434c72-0000.us-south.containers.appdomain.cloud   healthy

Router           Status
router-default   healthy

Secret                                          Namespace           Status
example-ae7743ca70a399d9cff4eaf617434c72-0000   ibm-cert-store      healthy
example-ae7743ca70a399d9cff4eaf617434c72-0000   openshift-ingress   healthy
```
{: screen}







The **Ingress Status** and **Ingress Message** fields are also returned in the output of the `ibmcloud oc cluster get` command. 
{: tip}


## Ingress statuses
{: #ingress_status}

The Ingress Status reflects the overall health of the Ingress components.
{: shortdesc}

| Ingress status | Description |
|--- | --- |
| `healthy` | The Ingress components are healthy.|
| `warning` | Some Ingress components might not function properly.|
| `critical` | Some Ingress components are malfunctioning.|
| `disabled` | Ingress status reporting is disabled. You can turn it on using the `ibmcloud oc ingress status-report enable` command.|
| `unsupported`| Ingress status reporting is not available for unsupported cluster versions. |
| `unknown`| The system is unable to calculate the Ingress status. |
{: caption="Ingress statuses" caption-side="bottom"}


## Ingress messages
{: #ingress_message}

The Ingress message provides details of what operation is in progress or information about any components that are unhealthy. Each status and message is described in the following tables.
{: shortdesc}

|Ingress message|Description|
|--- |--- |
| `The Ingress Operator is missing from the cluster. (ERRIONF).` | For more information, see [Why does the Ingress status show an ERRIONF error?](/docs/openshift?topic=openshift-ts-ingress-errionf).|
| `The Ingress Operator is in a degraded state (ERRIODEG).` | For more information, see [Why does the Ingress status show an ERRIODEG error?](/docs/openshift?topic=openshift-ts-ingress-erriodeg). |
| `One or more routes not admitted (ERRRNA).` | For more information, see [Why does the Ingress status show an ERRRNA error?](/docs/openshift?topic=openshift-ts-ingress-errrna).|
| `The external service is missing (ERRESNF).` | For more information, see [Why does the Ingress status show an ERRESNF error?](/docs/openshift?topic=openshift-ts-ingress-erresnf).|
| `The service is missing one or more worker IPs (ERRSEIPM).` | For more information, see [Why does the Ingress status show an ERRSEIPM error?](/docs/openshift?topic=openshift-ts-ingress-errseipm).|
| `The load balancer service address is missing (ERRSAM).` | For more information, see [Why does the Ingress status show an ERRSAM error?](/docs/openshift?topic=openshift-ts-ingress-errsam).|
| `Could not access {{site.data.keyword.secrets-manager_short}} instance (ESSSMI).` | For more information, see [Why does the Ingress status show an ESSSMI error?](/docs/openshift?topic=openshift-ts-ingress-esssmi).|
| `Could not access the secret group (ESSSMG).` | For more information, see [Why does the Ingress status show an ESSSMG error?](/docs/openshift?topic=openshift-ts-ingress-esssmg).|
| `The CRN does not match the default secret with the same domain (ESSVC).` | For more information, see [Why does the Ingress status show an ESSVC error?](/docs/openshift?topic=openshift-ts-ingress-essvc).|
| `The certificate for TLS secret expired or will expire soon (ESSEC).` | For more information, see [Why does the Ingress status show an ESSEC error?](/docs/openshift?topic=openshift-ts-ingress-essec).|
| `The Opaque secret field expired or will expire soon (ESSEF).` | For more information, see [Why does the Ingress status show an ESSEF error?](/docs/openshift?topic=openshift-ts-ingress-essef).|
| `The secret status shows a warning (ESSWS).` | For more information, see [Why does the Ingress status show an ESSWS error?](/docs/openshift?topic=openshift-ts-ingress-essws).|
| `The secret is not present on the cluster or is in the wrong namespace (ESSDNE).` | For more information, see [Why does the Ingress status show an ESSDNE error?](/docs/openshift?topic=openshift-ts-ingress-essdne).|
| `The external provider for the given subdomain has authorization issues (ERRDSAISS).` | For more information, see [Why does the Ingress status show an ERRDSAISS error?](/docs/openshift?topic=openshift-ts-ingress-errdsaiss)|
| `The subdomain has TLS secret issues (ERRDSISS).` | For more information, see [Why does the Ingress status show an ERRDSISS error?](/docs/openshift?topic=openshift-ts-ingress-errdsiss).|
| `The subdomain has DNS resolution issues (ERRDRISS).` | For more information, see [Why does the Ingress status show an ERRDRISS error?](/docs/openshift?topic=openshift-ts-ingress-errdriss).|
| `The subdomain has incorrect addresses registered (ERRDSIA).` | For more information, see [Why does the Ingress status show an ERRDSIA error?](/docs/openshift?topic=openshift-ts-ingress-errdsia).|
| `Invalid value for ALB version. (E0061).` | Before updating an ALB, check the list of ingress image versions available in the region using the command `ibmcloud ks ingress alb versions --region <region_id>`. For more information, see [Managing ALBs](/docs/openshift?topic=openshift-ingress-alb-manage).|
{: caption="Ingress messages" caption-side="bottom"}
