---

copyright: 
  years: 2023, 2023
lastupdated: "2023-06-27"

keywords: openshift, pod security, reset, valid configuration, psa

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



## Why do I get an error that my PodSecurityConfiguration is not valid?
{: #ts-pod-security-reset}
{: support}


When you use the `ibmcloud ks cluster master pod-security set` command with the `--config-file` option, you see an error similar to the following example.
{: tsSymptoms}

```sh
`The 'configuration' field is not a valid Kubernetes PodSecurityConfiguration setting. See 'http://ibm.biz/iks-psa-config' for more information.
```
{: screen}


There is a problem with the pod security configuration file. The content of this file is described in [Pod Security Admission plug-in configuration](/docs/containers?topic=containers-pod-security-admission#psa-plugin-config).
{: tsCauses}

Types of errors can include:
- YAML formatting errors such as indentation or using tab characters instead of spaces for indentation.
- The `apiVersion` or `kind` fields are missing or have incorrect values.
- A field name is not spelled correctly.
- A field has an incorrect value.

Check the configuration file for these kinds of errors. Correct any errors you find and try the command again.
{: tsResolve}


