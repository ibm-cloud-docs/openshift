---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-06"

keywords: openshift, roks, rhoks, rhos, responsibilities, incident, operations, change, security, regulation, disaster recovery, management

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Your responsibilities with using Red Hat OpenShift on IBM Cloud
{: #responsibilities_iks}
{: help}
{: support}

Learn about cluster management responsibilities that you have when you use {{site.data.keyword.openshiftlong}}. For overall terms of use, see [Cloud Services terms](/docs/overview/terms-of-use?topic=overview-terms#terms).
{: shortdesc}


IBM provides you with an enterprise cloud platform for you to deploy apps alongside {{site.data.keyword.cloud_notm}} DevOps, AI, data, and security services. You choose how you set up, integrate, and operate your apps and services in the cloud.

<table summary="The table shows the responsibilities of IBM and you. Rows are to be read from the left to right, with icons representing each responsibility in column one the description in column two.">
<caption>Responsibilities of IBM and you</caption>
  <thead>
  <th colspan=2>Responsibilities by type</th>
  </thead>
  <tbody>
    <tr>
    <td align="center"><img src="images/icon_clouddownload.svg" alt="Icon of a cloud with an arrow pointing down"/><br>Cloud infrastructure</td>
    <td>
    **IBM responsibilities**:
    <ul><li>Deploy a fully managed, highly available dedicated master in a secured, IBM-owned infrastructure account for each cluster.</li>
    <li>Provision worker nodes in your IBM Cloud infrastructure account.</li>
    <li>Set up cluster management components, such as VLANs and load balancers.</li>
    <li>Fulfill requests for more infrastructure, such as adding and removing worker nodes, creating default subnets, and provisioning storage volumes in response to persistent volume claims.</li>
    <li>Integrate ordered infrastructure resources to work automatically with your cluster architecture and become available to your deployed apps and workloads.</li></ul>
    <br><br>
    **Your responsibilities**:
    <ul><li>Use the provided API, CLI, or console tools to adjust [compute](/docs/openshift?topic=openshift-add_workers) and [storage](/docs/openshift?topic=openshift-storage_planning#storage_planning) capacity, and to adjust [networking configuration](/docs/openshift?topic=openshift-cs_network_cluster#cs_network_cluster) to meet the needs of your workload.</li></ul><br><br>
    </td>
     </tr>
     <tr>
     <td align="center"><img src="images/icon_tools.svg" alt="Icon of a wrench"/><br>Managed cluster</td>
     <td>
     **IBM responsibilities**:
     <ul><li>Provide a suite of tools to automate cluster management, such as the Red Hat OpenShift on IBM Cloud [API ![External link icon](../icons/launch-glyph.svg "External link icon")](https://containers.cloud.ibm.com/global/swagger-global-api/), [CLI plug-in](/docs/openshift?topic=openshift-kubernetes-service-cli), and [console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/clusters).</li>
     <li>Automatically apply Kubernetes master patch OS, version, and security updates. Make major and minor updates available for you to apply.</li>
     <li>Update and recover operational Red Hat OpenShift on IBM Cloud and Kubernetes components within the cluster, such as the Ingress application load balancer and file storage plug-in.</li>
     <li>Back up and recover data in etcd, such as your Kubernetes workload configuration files</li>
     <li>Set up an OpenVPN connection between the master and worker nodes when the cluster is created.</li>
     <li>Monitor and report the health of the master and worker nodes in the various interfaces.</li>
     <li>Provide worker node major, minor, and patch OS, version, and security updates.</li>
     <li>Fulfill automation requests to update and recover worker nodes. Provide the optional [worker node Autorecovery](/docs/openshift?topic=openshift-health#autorecovery).</li>
     </ul>
     <br><br>
     **Your responsibilities**:
     <ul>
     <li>Use the API, CLI, or console tools to [apply](/docs/openshift?topic=openshift-update#update) the provided major and minor Kubernetes master updates and major, minor, and patch worker node updates.</li>
     <li>Use the API, CLI, or console tools to [recover](/docs/openshift?topic=openshift-cs_troubleshoot) your infrastructure resources.</li></ul>
     <br><br></td>
      </tr>
    <tr>
      <td align="center"><img src="images/icon_locked.svg" alt="Icon of lock"/><br>Security-rich environment</td>
      <td>
      **IBM responsibilities**:
      <ul>
      <li>Maintain controls commensurate to [various industry compliance standards](/docs/containers?topic=containers-faqs#standards), such as PCI DSS.</li>
      <li>Monitor, isolate, and recover the cluster master.</li>
      <li>Provide highly available replicas of the Kubernetes master API server, etcd, scheduler, and controller manager components to protect against a master outage.</li>
      <li>Automatically apply master security patch updates, and provide worker node security patch updates.</li>
      <li>Enable certain security settings, such as encrypted disks on worker nodes</li>
      <li>Disable certain insecure actions for worker nodes, such as not permitting users to SSH into the host.</li>
      <li>Encrypt communication between the master and worker nodes with TLS.</li>
      <li>Provide CIS-compliant Linux images for worker node operating systems.</li>
      <li>Continuously monitor master and worker node images to detect vulnerability and security compliance issues.</li>
      <li>Provision worker nodes with two local SSD, AES 256-bit encrypted data partitions.</li>
      <li>Provide options for cluster network connectivity, such as public and private service endpoints.</li>
      <li>Provide options for compute isolation, such as dedicated virtual machines or bare metal.</li>
      <li>Integrate Kubernetes role-based access control (RBAC) with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).</li>
      </ul>
      <br><br>
      **Your responsibilities**:
      <ul>
      <li>Use the API, CLI, or console tools to apply the provided [security patch updates](/docs/openshift?topic=openshift-openshift_changelog) to your worker nodes.</li>
      <li>Choose how to set up your [cluster network](/docs/openshift?topic=openshift-plan_clusters) and configure further [security settings](/docs/openshift?topic=openshift-security#security) to meet your workload's security and compliance needs. If applicable, configure your [firewall](/docs/openshift?topic=openshift-firewall#firewall).</li></ul>
      <br><br></td>
      </tr>

      <tr>
        <td align="center"><img src="images/icon_code.svg" alt="Icon of code brackets"/><br>App orchestration</td>
        <td>
        **IBM responsibilities**:
        <ul>
        <li>Provision clusters with Kubernetes components installed so that you can access the Kubernetes API.</li>
        <li>Provide a number of managed add-ons to extend your app's capabilities, such as the Kubernetes web terminal or the Diagnostics and Debug Tool. Maintenance is simplified for you because IBM provides the installation and updates for the managed add-ons.</li>
        <li>Provide cluster integration with select third-party partnership technologies, such as {{site.data.keyword.la_short}}, {{site.data.keyword.mon_short}}, and Portworx.</li>
        <li>Provide automation to enable service binding to other {{site.data.keyword.cloud_notm}} services.</li>
        <li>Create clusters with image pull secrets so that your deployments in the `default` Kubernetes namespace can pull images from {{site.data.keyword.registrylong_notm}}.</li>
        <li>Provide storage classes and plug-ins to support persistent volumes for use with your apps.</li>
        <li>Create clusters with subnet IP addresses reserved to use to expose apps externally.</li>
        <li>Support native Kubernetes public and private load balancers and Ingress routes for exposing services externally.</li>
        </ul>
        <br><br>
        **Your responsibilities**:
        <ul>
        <li>Use the provided tools and features to [configure and deploy](/docs/openshift?topic=openshift-openshift_apps); [set up permissions](/docs/openshift?topic=openshift-users#users); [integrate with other services](/docs/openshift?topic=openshift-openshift_integrations); [externally serve](/docs/containers?topic=openshift-cs_network_planning); [set up and monitor the health](/docs/openshift?topic=openshift-health); [save, back up, and restore data](/docs/openshift?topic=openshift-storage_planning#storage_planning); and otherwise manage your [highly available](/docs/openshift?topic=openshift-ha#ha) and resilient workloads.</li>
        </ul>
        </td>
        </tr>
  </tbody>
  </table>




