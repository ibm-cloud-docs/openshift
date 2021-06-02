---

copyright:
  years: 2014, 2021
lastupdated: "2021-06-02"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
  
  
# After deleting all worker nodes, why don't my pods start on new worker nodes?
{: #zero_nodes_calico_failure}

**Infrastructure provider**:
  * <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
You deleted all worker nodes in your cluster so that zero worker nodes exist. Then, you added one or more worker nodes. When you run the following command, several pods for Kubernetes components are stuck in the `ContainerCreating` status, and the `calico-node` pods are stuck in the `CrashLoopBackOff` status.

```
oc -n kube-system get pods
```
{: pre}

{: tsCauses}
When you delete all worker nodes in your cluster, no worker node exists for the `calico-kube-controllers` pod to run on. The Calico controller pod's data cannot be updated to remove the data of the deleted worker nodes. When the Calico controller pod begins to run again on the new worker nodes, its data is not updated for the new worker nodes, and it does not start the `calico-node` pods.

{: tsResolve}
Delete the existing `calico-node` worker node entries so that new pods can be created.

**Before you begin**: Install the [Calico CLI](/docs/openshift?topic=openshift-network_policies#cli_install).

1. Run the `ibmcloud oc cluster config` command and copy and paste the output to set the `KUBECONFIG` environment variable. Include the `--admin` and `--network` options with the `ibmcloud oc cluster config` command. The `--admin` option downloads the keys to access your infrastructure portfolio and run Calico commands on your worker nodes. The `--network` option downloads the Calico configuration file to run all Calico commands.
  ```
  ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin --network
  ```
  {: pre}

2. For the `calico-node` pods that are stuck in the `CrashLoopBackOff` status, note the `NODE` IP addresses.
  ```
  oc -n kube-system get pods -o wide
  ```
  {: pre}

  In this example output, the `calico-node` pod cannot start on worker node `10.176.48.106`.
  ```
  NAME                                           READY   STATUS              RESTARTS   AGE     IP              NODE            NOMINATED NODE   READINESS GATES
  ...
  calico-kube-controllers-656c5785dd-kc9x2       1/1     Running             0          25h     10.176.48.107   10.176.48.107   <none>           <none>
  calico-node-mkqbx                              0/1     CrashLoopBackOff    1851       25h     10.176.48.106   10.176.48.106   <none>           <none>
  coredns-7b56dd58f7-7gtzr                       0/1     ContainerCreating   0          25h     172.30.99.82    10.176.48.106   <none>           <none>
  ```
  {: screen}

3. Get the IDs of the `calico-node` worker node entries. Copy the IDs for **only** the worker node IP addresses that you retrieved in the previous step.
  ```
  calicoctl get nodes -o wide
  ```
  {: pre}

4. Use the IDs to delete the worker node entries. After you delete the worker node entries, the Calico controller reschedules the `calico-node` pods on the new worker nodes.
  ```
  calicoctl delete node <node_ID>
  ```
  {: pre}

5. Verify that the Kubernetes component pods, including the `calico-node` pods, are now running. It might take a few minutes for the `calico-node` pods to be scheduled and for new component pods to be created.
  ```
  oc -n kube-system get pods
  ```
  {: pre}

To prevent this error in the future, never delete all worker nodes in your cluster. Always run at least one worker node in your cluster, and if you use Ingress or routes to expose apps, run at least two worker nodes per zone.
{: note}


