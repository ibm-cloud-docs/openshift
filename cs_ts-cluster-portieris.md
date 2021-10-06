---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-06"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why is my Portieris cluster image security enforcement installation canceled?
{: #portieris_enable}

**Infrastructure provider**:
    * ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
    * ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC


Portieris image security enforcement add-on does not install.  You see a master status similar to the following:
{: tsSymptoms}

```
Image security enforcement update cancelled. CAE008: Cannot enable Portieris image security enforcement because the cluster already has a conflicting image admission controller installed. For more information, see the troubleshooting docs: 'https://ibm.biz/portieris_enable'
```
{: screen}


Your cluster has a conflicting image admission controller already installed, which prevents the image security enforcement cluster add-on from installing.
{: tsCauses}

When you have more than one image admission controller in your cluster, pods might not run.

Potential conflicting image admission controller sources include:
*   The deprecated container image security enforcement Helm chart.
*   A previous manual installation of the open source [Portieris](https://github.com/IBM/portieris){: external} project.


Identify and remove the conflicting image admission controller.
{: tsResolve}

1. Check for existing image admission controllers.
    *   Check if you have an existing container image security enforcement deployment in your cluster. If no output is returned, you do not have the deployment.
        ```sh
        oc get deploy cise-ibmcloud-image-enforcement -n ibm-system
        ```
        {: pre}

        Example output
        ```sh
        NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
        cise-ibmcloud-image-enforcement   3/3     3            3           129m
        ```
        {: pre}

    *   Check if you have an existing Portieris deployment in your cluster. If no output is returned, you do not have the deployment.
        ```sh
        oc get deployment --all-namespaces -l app=portieries
        ```
        {: pre}

        Example output
        ```sh
        NAMESPACE     NAME        READY   UP-TO-DATE   AVAILABLE   AGE
        portieris     portieris   3/3     3            3           8m8s
        ```
        {: pre}

2. Uninstall the conflicting deployment.
    ```sh
    oc delete deployment <deployment> -n <namespace>
    ```
    {: pre}
    
3. Confirm that conflicting admission controllers are removed by checking that the cluster no longer has a mutating webhook configuration for an image admission controller.
    ```sh
    oc get MutatingWebhookConfiguration image-admission-config
    ```
    {: pre}

    Example output

    ```sh
    Error from server (NotFound): mutatingwebhookconfigurations.admissionregistration.k8s.io "image-admission-config" not found
    ```
    {: pre}

4. Retry the installing the add-on by running the `ibmcloud oc cluster image-security enable` command.



