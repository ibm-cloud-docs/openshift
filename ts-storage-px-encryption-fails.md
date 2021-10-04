---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-04"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---
{{site.data.keyword.attribute-definition-list}}



# Why does encryption fail with an invalid KMS endpoint?
{: #px-kms-endpoint}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


When you provision Portworx and set up encryption, you receive an error similar to the following:
{: tsSymptoms}

```sh
`kp.Error: correlation_id='673bb68a-be17-4720-9ae1-85baf109924e', msg='Unauthorized: The user does not have access to the specified resource'"`
```
{: screen}


The endpoint that you entered in your Kubernetes secret is incorrect. If the KMS endpoint is entered incorrectly, Portworx cannot access the KMS provider that you configured.
{: tsCauses}

For more information about enabling encryption on your Portworx volumes, see [Setting up encryption](/docs/openshift?topic=openshift-portworx#encrypt_volumes).


Edit your Kubernetes secret to include the correct endpoint for your KMS provider.
{: tsResolve}

1. Retrieve the correct endpoint for your KMS provider.

    * **{{site.data.keyword.keymanagementservicelong_notm}}**: [Retrieve the region](/docs/key-protect?topic=key-protect-regions#regions) where you created your service instance. Make sure that you note your API endpoint in the correct format. Example: `https://us-south.kms.cloud.ibm.com`.
    * **{{site.data.keyword.hscrypto}}**: [Retrieve the Key Management public endpoint URL](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). Make sure that you note your endpoint in the correct format. Example: `https://api.us-south.hs-crypto.cloud.ibm.com:<port>`. For more information, see the [{{site.data.keyword.hscrypto}} API documentation](https://cloud.ibm.com/apidocs/hs-crypto#getinstance).

2. Encode the endpoint to base64.
    ```sh
    echo -n "<endpoint>" | base64
    ```
    {: pre}

3. [Edit the Kubernetes secret that you created to include the correct endpoint for your KMS provider](/docs/openshift?topic=openshift-portworx#px_create_km_secret).
    ```sh
    oc edit <secret-name> -n portworx
    ```
    {: pre}

4. Save and close your Kubernetes secret to reapply it to your cluster.


If you find information that you entered incorrectly or you must change the setup of your cluster, correct the information or the cluster setup.
{: note}






