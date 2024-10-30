---

copyright: 
  years: 2024, 2024
lastupdated: "2024-10-30"


keywords: kubernetes, openshift, MountingTargetFailed, encryption in-transit, eit

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Why does PVC creation fail for {{site.data.keyword.filestorage_vpc_short}}?
{: #ts-storage-vpc-file-eit-pvc-fails}

[Virtual Private Cloud]{: tag-vpc}

PVC creation fails with an error message similar to the following.
{: tsSymptoms}

```sh
vpc.file.csi.ibm.io_ibm-vpc-file-csi-controller-699b96b98-7vhwx_58851c95-cfcc-461c-8fac-2fdecc146cb4  failed to provision volume with StorageClass "ibmc-vpc-file-dp2": rpc error: code = FailedPrecondition desc = {RequestID: 4c7b91e2-3e09-4164-9620-2ae95b2df4dd , Code: SubnetFindFailed, Description: A subnet with the specified zone 'jp-osa-2' and available cluster subnet list '02o7-b4ff2863-3b9f-4264-9b58-0b8272172db7,02p7-1708554a-b471-4e6e-8092-7b9e958f4418,02n7-54f9b149-629c-4d43-9a87-7b8f0831f159' could not be found., BackendError: {Code:SubnetFindFailed, Type:RetrivalFailed, Description:A subnet with the specified zone 'jp-osa-2' and available cluster subnet list '02o7-b4ff2863-3b9f-4264-9b58-0b8272172db7,02p7-1708554a-b471-4e6e-8092-7b9e958f4418,02n7-54f9b149-629c-4d43-9a87-7b8f0831f159' could not be found., BackendError:no subnet found, RC:404}, Action: Please check if the property 'vpc_subnet_ids' contains valid subnetIds. Please check 'kubectl get configmap ibm-cloud-provider-data -n kube-system -o yaml'.Please check 'BackendError' tag for more details}
```
{: screen}


One possible cause for this issue is that your Cluster and VPC are in different resource groups. If this is true, create your own storage class and retry creating a PVC. If your cluster and VPC are in the same resource group, verify your subnet details, then open a support case and provide your VPC subnet information.
{: tsResolve}


1. Find the resource group of your cluster and VPC. You can find your resource groups in the console or by running the `ibmcloud is resource service-instances -g GROUP` command.


    * **Cluster and VPC are not in the same resource group**: [Create your own storage class](/docs/openshift?topic=openshift-storage-file-vpc-apps#storage-file-vpc-custom-sc) and make sure to specify the VPC resource group ID in the `resourceGroup` section as well as the `kube-<clusterID>` security group ID in the `securityGroupIDs` section. You can find the ID of the `kube-<clusterID>` security group by running the following command.
        ```sh
        ibmcloud is sg kube-<cluster-id>  | grep ID
        ```
        {: pre}


    * **Cluster and VPC are in the same resource group**: Check that the `vpc_subnet_ids` property contains valid subnet IDs.

        1. Review the subnet IDs in the `ibm-cloud-provider-data` configmap. 
            ```sh
            oc get cm ibm-cloud-provider-data -n kube-system -o yaml | grep vpc_subnet_ids
            ```
            {: pre}


        1. Verify that the subnet IDs you found in the previous step exist.

            ```sh
            ibmcloud is subnets | grep <zone-name>
            ```
            {: pre}

1. If the issue persists, Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
