---

copyright: 
  years: 2014, 2021
lastupdated: "2021-10-19"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why can't I view or work with my cluster?
{: #cs_cluster_access}

**Infrastructure provider**:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC

You are not able to find a cluster. When you run `ibmcloud oc cluster ls`, the cluster is not listed in the output.
{: tsSymptoms}

Or, you are not able to work with a cluster. When you run `ibmcloud oc cluster config` or other cluster-specific commands, the cluster is not found.



In {{site.data.keyword.cloud_notm}}, each resource must be in a resource group. For example, cluster `mycluster` might exist in the `default` resource group.
{: tsCauses} 

When the account owner gives you access to resources by assigning you an {{site.data.keyword.cloud_notm}} IAM platform access role, the access can be to a specific resource or to the resource group. When you are given access to a specific resource, you don't have access to the resource group. In this case, you don't need to target a resource group to work with the clusters you have access to. If you target a different resource group than the group that the cluster is in, actions against that cluster can fail. Conversely, when you are given access to a resource as part of your access to a resource group, you must target a resource group to work with a cluster in that group. If you don't target your CLI session to the resource group that the cluster is in, actions against that cluster can fail.

If you cannot find or work with a cluster, you might be experiencing one of the following issues:
* You have access to the cluster and the resource group that the cluster is in, but your CLI session is not targeted to the resource group that the cluster is in.
* You have access to the cluster, but not as part of the resource group that the cluster is in. Your CLI session is targeted to this or another resource group.
* You don't have access to the cluster.


To check your user access permissions:
{: tsResolve}

1. List all of your user permissions.
    ```sh
    ibmcloud iam user-policies <your_user_name>
    ```
    {: pre}

2. Check if you have access to the cluster and to the resource group that the cluster is in.
    1. Look for a policy that has a **Resource Group Name** value of the cluster's resource group and a **Memo** value of `Policy applies to the resource group`. If you have this policy, you have access to the resource group. For example, this policy indicates that a user has access to the `test-rg` resource group:
        ```sh
        Policy ID:   3ec2c069-fc64-4916-af9e-e6f318e2a16c
        Roles:       Viewer
        Resources:
        Resource Group ID     50c9b81c983e438b8e42b2e8eca04065
        Resource Group Name   test-rg
        Memo                  Policy applies to the resource group
        ```
        {: screen}

    2. Look for a policy that has a **Resource Group Name** value of the cluster's resource group, a **Service Name** value of `containers-kubernetes` or no value, and a **Memo** value of `Policy applies to the resource(s) within the resource group`. If you this policy, you have access to clusters or to all resources within the resource group. For example, this policy indicates that a user has access to clusters in the `test-rg` resource group:
        ```sh
        Policy ID:   e0ad889d-56ba-416c-89ae-a03f3cd8eeea
        Roles:       Administrator
        Resources:
        Resource Group ID     a8a12accd63b437bbd6d58fb6a462ca7
        Resource Group Name   test-rg
        Service Name          containers-kubernetes
        Service Instance
        Region
        Resource Type
        Resource
        Memo                  Policy applies to the resource(s) within the resource group
        ```
        {: screen}

    3. If you have both of these policies, skip to Step 4, first bullet. If you don't have the policy from Step 2a, but you do have the policy from Step 2b, skip to Step 4, second bullet. If you do not have either of these policies, continue to Step 3.

3. Check if you have access to the cluster, but not as part of access to the resource group that the cluster is in.
    1. Look for a policy that has no values besides the **Policy ID** and **Roles** fields. If you have this policy, you have access to the cluster as part of access to the entire account. For example, this policy indicates that a user has access to all resources in the account:
        ```sh
        Policy ID:   8898bdfd-d520-49a7-85f8-c0d382c4934e
        Roles:       Administrator, Manager
        Resources:
        Service Name
        Service Instance
        Region
        Resource Type
        Resource
        ```
        {: screen}

    2. Look for a policy that has a **Service Name** value of `containers-kubernetes` and a **Service Instance** value of the cluster's ID. You can find a cluster ID by running `ibmcloud oc cluster get --cluster <cluster_name>`. For example, this policy indicates that a user has access to a specific cluster:
        ```sh
        Policy ID:   140555ce-93ac-4fb2-b15d-6ad726795d90
        Roles:       Administrator
        Resources:
        Service Name       containers-kubernetes
        Service Instance   df253b6025d64944ab99ed63bb4567b6
        Region
        Resource Type
        Resource
        ```
        {: screen}

    3. If you have either of these policies, skip to the second bullet point of step 4. If you do not have either of these policies, skip to the third bullet point of step 4.

4. Depending on your access policies, choose one of the following options. 

    - If you have access to the cluster and to the resource group that the cluster is in:
        1. Target the resource group. **Note**: You can't work with clusters in other resource groups until you untarget this resource group.
            ```sh
            ibmcloud target -g <resource_group>
            ```
            {: pre}

        2. Target the cluster.
            ```sh
            ibmcloud oc cluster config --cluster <cluster_name_or_ID>
            ```
            {: pre}

    - If you have access to the cluster but not to the resource group that the cluster is in:
        1. Do not target a resource group. If you already targeted a resource group, untarget it:
            ```sh
            ibmcloud target --unset-resource-group
            ```
            {: pre}

        2. Target the cluster.
            ```sh
            ibmcloud oc cluster config --cluster <cluster_name_or_ID>
            ```
            {: pre}

    - If you do not have access to the cluster:
        1. Ask your account owner to assign an [{{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-users#checking-perms) to you for that cluster.
        2. Do not target a resource group. If you already targeted a resource group, untarget it:
            ```sh
            ibmcloud target --unset-resource-group
            ```
            {: pre}

        3. Target the cluster.
            ```sh
            ibmcloud oc cluster config --cluster <cluster_name_or_ID>
            ```
            {: pre}



